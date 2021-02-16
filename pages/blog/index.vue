<template>
  <div class="mt-12 py-12 px-6 mb-4 md:p-20 leading-relaxed">
    <h1 class="text-4xl font-semibold">Blog</h1>
    <p class="text-xl">
      Putting my thoughts down on virtual paper + some of my personal and work
      projects.
    </p>
    <div class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 gap-6">
      <div
        class="transform duration-300 hover:scale-105"
        v-for="article of articles"
        :key="article.slug"
      >
        <NuxtLink :to="{ name: 'blog-slug', params: { slug: article.slug } }">
          <div class="mt-6 shadow-md rounded-lg">
            <div class="relative rounded-tl-lg rounded-tr-lg h-48">
              <img
                class="object-cover object-center rounded-tl-lg rounded-tr-lg h-full w-full"
                :src="article.img"
              />
            </div>
            <div class="py-3 px-6 bg-white rounded-lg">
              <h2 class="text-2xl font-semibold leading-snug">{{ article.title }}</h2>
              <!--<p class="text-gray-700">Written by {{article.author}} </br> -->
              <p>{{ article.date }}</p>
              <p class="mb-2">{{ article.description }}</p>
            </div>
          </div>
        </NuxtLink>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  transition: "fade",

  async asyncData({ $content, params }) {
    const articles = await $content("articles", params.slug)
      .only(["title", "description", "img", "date", "slug", "author", "order"])
      .sortBy("order", "desc")
      .fetch();

    console.log(articles);

    return {
      articles
    };
  },
  methods: {
    formatDate(date) {
      const options = { year: "numeric", month: "long", day: "numeric" };
      return new Date(date).toLocaleDateString("en", options);
    }
  }
};
</script>
