<template>
  <!-- container for fixed nav bar -->
  <div class="fixed z-20 w-full top-0" ref="navbar">
    <header
      class="py-2 md:py-1 lg:px-16 px-6 bg-white flex flex-wrap items-center shadow-md md:shadow-sm dark:bg-gray-800"
    >
      <div
        @click="closeBox"
        class="flex-1 flex justify-between items-center dark:text-white"
      >
        <nuxt-link
          to="/"
          exact
          active-class="text-indigo-600 dark:text-indigo-300"
          class="font-medium lg:p-4 md:my-0 py-3 block border-b-2 text-xl border-transparent hover:border-indigo-400"
        >
          <h2>
            NP
          </h2>
        </nuxt-link>
      </div>

      <label
        for="menu-toggle"
        class="cursor-pointer lg:hidden block"
        @click="onClick"
      >
        <div ref="container" class="text-white"></div>
      </label>
      <input class="hidden" type="checkbox" id="menu-toggle" />

      <div class="hidden lg:flex lg:items-center lg:w-auto w-full" id="menu">
        <nav>
          <ul
            class="lg:flex items-center justify-between text-base dark:text-white text-gray-700 pt-4 lg:pt-0"
          >
            <li v-for="nav in navs" :key="nav.to" @click="closeBox">
              <nuxt-link
                active-class="text-indigo-600 dark:text-indigo-300"
                :to="nav.to"
                class="lg:p-4 my-6 md:my-0 py-3 block border-b-2 text-xl border-transparent hover:border-indigo-400"
                >{{ nav.text }}</nuxt-link
              >
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
      animationData,
      rendererSettings: {
        className: "svgImage"
      }
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

<style lang="postcss">
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

.dark .svgImage {
  filter: invert(1);
}
</style>
