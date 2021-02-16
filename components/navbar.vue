<template>
  <!-- container for fixed nav bar -->
  <div class="fixed z-20 w-full top-0" ref="navbar">
    <header class="lg:px-16 px-6 bg-white flex flex-wrap items-center shadow-sm">
      <div class="flex-1 flex justify-between items-center">
        <nuxt-link to="/">
          <h2
            class="font-medium py-2 lg:p-3 text-xl border-b-2 border-transparent active:border-indigo-400 hover:border-indigo-400"
          >NP</h2>
        </nuxt-link>
      </div>

      <label for="menu-toggle" class="cursor-pointer lg:hidden block" @click="onClick">
        <div ref="container"></div>
      </label>
      <input class="hidden" type="checkbox" id="menu-toggle" />

      <div class="hidden lg:flex lg:items-center lg:w-auto w-full" id="menu">
        <nav>
          <ul class="lg:flex items-center justify-between text-base text-gray-700 pt-4 lg:pt-0">
            <li v-for="nav in navs" :key="nav.to" @click="closeBox">
              <nuxt-link
                :to="nav.to"
                class="lg:p-4 py-3 px-0 block border-b-2 border-transparent hover:border-indigo-600"
              >{{ nav.text }}</nuxt-link>
            </li>
          </ul>
        </nav>
      </div>
    </header>
  </div>
</template>

<script>
export default {
  data() {
    return {
      pngLogo: require("@/assets/logo.png"),
      menu: require("@/assets/menu.svg"),
      anim: null,
      animComplete: false,
      navs: [
        { text: "Blog", to: "/blog" },
        { text: "Reading", to: "/readings" },
        { text: "Contact", to: "/contact" }
      ]
    };
  },
  async mounted() {
    const animationData = await import("@/assets/menu.json");
    const lottie = await import("lottie-web");
    this.anim = lottie.loadAnimation({
      container: this.$refs.container,
      renderer: "svg",
      loop: false,
      autoplay: false,
      animationData
    });
    this.anim.setSpeed(2);
    this.anim.addEventListener("complete", () => {
      this.animComplete = true;
    });
  },
  methods: {
    onClick(evt) {
      console.log({ evt, anim: this.anim, dir: this.anim.playDirection });
      if (this.animComplete) {
        this.anim.setDirection(this.anim.playDirection * -1);
        this.anim.play();
      } else {
        this.anim.play();
      }
    },
    scroll(selector) {
      console.log({ selector });
      document.querySelector(selector).scrollIntoView();
    },
    closeBox() {
      const checkbox = document.querySelector("#menu-toggle");
      if (checkbox.checked) {
        this.anim.setDirection(-1);
        this.anim.play();
      }
      checkbox.checked = false;
    }
  },
  transition: "fade"
};
</script>

<style>
#menu-toggle:checked + #menu {
  display: block;
}
html {
  scroll-behavior: smooth;
}

.fade-in {
  opacity: 1;
  animation-name: fadeInOpacity;
  animation-iteration-count: 1;
  animation-timing-function: ease-in;
  animation-duration: 1s;
}

@keyframes fadeInOpacity {
  0% {
    opacity: 0;
  }
  100% {
    opacity: 1;
  }
}
a.nuxt-link-exact-active {
  color: #4f46e5;
}
</style>
