<template>
  <div class="w-full h-screen relative fade-in p-8 md:p-20 leading-relaxed">
      <h1 class="font-bold text-5xl mt-12 py-12 px-8 mb-4 md:p-20 2xl:mt-32">Nik Paradis</h1>
      <div v-if="!isMobile">
        <p class="text-2xl">
          A UX Designer turned PM. I focus on making great experiences happen. I love
          <client-only>
            <vue-typer class="text-2xl" :text="textData" :type-delay="150" />
          </client-only>
        </p>
      </div>

      <div v-else>
        <p class="text-2xl">
          A UX Designer turned PM. I focus on making great experiences happen. </br> I love
          <client-only>
            <vue-typer class="text-2xl"
              :text='["Books.","Bitcoin.","Board Games."]'
              :repeat='Infinity'
              :shuffle='false'
              initial-action='typing'
              :pre-type-delay='70'
              :type-delay='100'
              :pre-erase-delay='1500'
              :erase-delay='250'
              erase-style='select-all'
              :erase-on-complete='false'
              caret-animation='blink'
            ></vue-typer>
          </client-only>
        </p>
      </div>

      <a target="_blank" href="/resume.pdf">
        <button
          class="rounded-lg text-lg px-10 mt-8 py-3 bg-indigo-600 hover:bg-indigo-700 text-white font-medium relative"
        >
          See My Resume
          <span class="flex h-3 w-3 absolute right-0" style="top: -5px">
            <span
              class="animate-ping absolute h-4 w-4 rounded-full bg-indigo-400 opacity-75"
            ></span>
            <span
              class="absolute inline-flex rounded-full h-4 w-4 bg-indigo-500"
            ></span>
          </span>
        </button>
      </a>

      <!--projects arrow -->
      <div class="text-center animate-pulse text-4xl m-auto block mt-24 md:mt-40 mb-12">
        <nuxt-link to="/blog">&#8594;</nuxt-link>
      </div>
    </div>

</template>
<script>
export default {
  transition: "fade",

  components: {
    VueTyper: () => import("vue-typer").then(m => m.VueTyper)
  },
  data() {
    return {
      isMobile: false,
      textData: ["Books.", "Bitcoin.", "Board Games."]
    };
  },
  mounted() {
    const w = window.innerWidth;
    this.isMobile = w < 750;
    window.addEventListener("resize", () => {
      const w = window.innerWidth;
      this.isMobile = w < 750;
    });
  }
};
</script>

<style>
  .vue-typer,
  .custom.char.typed {
    color: #4f46e5;
  }
</style>
