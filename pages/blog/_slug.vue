<template>
  <article
    class="py-16 px-6 md:p-20 w-full leading-relaxed bg-white dark:bg-gray-800 dark:text-white min-h-screen"
  >
    <div class="max-w-4xl m-auto mt-12">
      <nuxt-link class="text-lg hover:underline" to="/blog"
        >&#8592; back to posts</nuxt-link
      >
      <h1 class="text-4xl font-semibold leading-tight mt-2">
        {{ article.title }}
      </h1>
      <p class="text-gray-700 dark:text-gray-50">
        Written by {{ article.author }}
      </p>
      <p class="text-gray-700 dark:text-gray-50 mb-2">{{ article.date }}</p>
      <div class="h-56 my-4">
        <img
          class="object-cover object-center rounded-md h-full w-full"
          :src="article.img"
        />
      </div>
      <nuxt-content class="leading-relaxed list-decimal" :document="article" />
      <applause-button
        multiclap="true"
        color="#7c3aed"
        class="mt-12 mb-6 mx-auto"
        style="width: 58px; height: 58px;"
      />
      <prev-next class="mt-4 text-xl" :prev="prev" :next="next" />
    </div>
  </article>
</template>

<style lang="postcss">
.nuxt-content h2 {
  font-weight: 600;
  font-size: 28px;
  margin-top: 3rem;
  margin-bottom: 1rem;
}
.nuxt-content h3 {
  font-weight: bold;
  font-size: 22px;
}
.nuxt-content p {
  margin-bottom: 20px;
  font-size: 22px;
}

.nuxt-content blockquote {
  @apply my-16;
  @apply mx-2;
  @apply px-6;
  @apply py-2;
  @apply border-l-8;
  @apply italic;
  @apply border-indigo-600;
}
.nuxt-content blockquote p {
  margin-bottom: 0px;
}

.dark .nuxt-content blockquote {
  @apply border-indigo-300;
}

.nuxt-content ol {
  @apply text-xl;
  @apply list-inside;
  @apply ml-2;
  @apply mb-4;
}
.nuxt-content li {
  @apply mb-2;
  @apply list-decimal;
}

.dark applause-button .style-root {
  stroke: #c4b5fd !important;
  fill: #c4b5fd !important;
  color: #c4b5fd !important;
}
</style>

<script>
export default {
  head: {
    script: [
      {
        src: "https://unpkg.com/applause-button/dist/applause-button.js"
      }
    ],
    link: [
      {
        rel: "stylesheet",
        href: "https://unpkg.com/applause-button/dist/applause-button.css"
      }
    ]
  },
  async asyncData({ $content, params }) {
    // fetch our article here
    const article = await $content("articles", params.slug).fetch();
    console.log(article);
    const [prev, next] = await $content("articles")
      .only(["title", "slug", "img"])
      .sortBy("createdAt", "asc")
      .surround(params.slug)
      .fetch();

    return { article, prev, next };
  },

  methods: {
    formatDate(date) {
      const options = { year: "numeric", month: "long", day: "numeric" };
      return new Date(date).toLocaleDateString("en", options);
    }
  }
};
</script>
