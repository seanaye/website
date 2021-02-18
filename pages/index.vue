<template>
  <div class="w-full relative fade-in py-16 px-6 md:p-20 leading-relaxed dark:bg-gray-800 dark:text-white min-h-screen">
      <h1 class="font-bold text-5xl mt-12 md:mt-12 mb-6">Nik Paradis</h1>
      <div v-if="!isMobile">
        <p class="text-2xl">
          A UX Designer turned PM. I focus on making great experiences happen. I love
          <client-only>
             <vue-typer class="text-2xl"
              :text='["Books.","Bitcoin.","Board Games."]'
              :repeat='Infinity'
              :shuffle='false'
              initial-action='typing'
              :pre-type-delay='75'
              :type-delay='100'
              :pre-erase-delay='1200'
              :erase-delay='250'
              erase-style='select-all'
              :erase-on-complete='false'
              caret-animation='blink'
            ></vue-typer>
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
              :pre-type-delay='75'
              :type-delay='100'
              :pre-erase-delay='1000'
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

   <!-- This is an example component -->
      <button @click="switchTheme" class="block mt-32 md:mt-40 mb-12 h-10 w-10 mx-auto focus:outline-none text-gray-900">
        <svg id="moon" class="p-4" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20" fill="currentColor">
          <path d="M17.293 13.293A8 8 0 016.707 2.707a8.001 8.001 0 1010.586 10.586z" />
        </svg>
        <svg id="sun" class="hidden p-4 text-yellow-500" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20" fill="currentColor">
          <path fill-rule="evenodd" d="M10 2a1 1 0 011 1v1a1 1 0 11-2 0V3a1 1 0 011-1zm4 8a4 4 0 11-8 0 4 4 0 018 0zm-.464 4.95l.707.707a1 1 0 001.414-1.414l-.707-.707a1 1 0 00-1.414 1.414zm2.12-10.607a1 1 0 010 1.414l-.706.707a1 1 0 11-1.414-1.414l.707-.707a1 1 0 011.414 0zM17 11a1 1 0 100-2h-1a1 1 0 100 2h1zm-7 4a1 1 0 011 1v1a1 1 0 11-2 0v-1a1 1 0 011-1zM5.05 6.464A1 1 0 106.465 5.05l-.708-.707a1 1 0 00-1.414 1.414l.707.707zm1.414 8.486l-.707.707a1 1 0 01-1.414-1.414l.707-.707a1 1 0 011.414 1.414zM4 11a1 1 0 100-2H3a1 1 0 000 2h1z" clip-rule="evenodd" />
        </svg>
      </button>

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
      isMobile: false
    };
  },
  mounted() {
    const w = window.innerWidth;
    this.isMobile = w < 750;
    window.addEventListener("resize", () => {
      const w = window.innerWidth;
      this.isMobile = w < 750;
    });
  },

  methods: {
    switchTheme() {
      let htmlClasses = document.querySelector('html').classList;

      if(localStorage.theme == 'dark'){
        htmlClasses.remove('dark');
        localStorage.removeItem('theme');
      } else {
        htmlClasses.add('dark');
        localStorage.theme = 'dark';
      }

      var sun = document.getElementById("sun");
      var moon = document.getElementById("moon");
      
      sun.classList.toggle('hidden');
      moon.classList.toggle('hidden');

    }

  },
  //ensure proper svg is shown
    beforeUpdate(){
      var sun = document.getElementById("sun");
      var moon = document.getElementById("moon");
      if (localStorage.theme == 'dark'){
        let htmlClasses = document.querySelector('html').classList;
        htmlClasses.add('dark');
        console.log("am run dark");
        if (sun.classList.contains('hidden')){
          moon.classList.toggle('hidden');
          sun.classList.toggle('hidden');
        };
      }
    }
};
</script>

<style>
  body {
    transition: 2s; 
  }

  .custom.char.typed {
    color: #4f46e5;
  }

  .dark .custom.char.typed {
    color: #A5B4FC;
  }
  
  .dark .vue-typer .custom.caret {
  background-color: white;
}

  .fade-enter-active,
  .fade-leave-active {
    transition: opacity 0.5s;
  }
  .fade-enter,
  .fade-leave-active {
    opacity: 0;
  }
</style>
