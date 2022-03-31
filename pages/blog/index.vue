<template>
  <article>
    <section class="text-gray-900 body-font">
      <div class="container px-5 mx-auto">
        <h1 class="text-left py-12 font-bold font-sans text-4xl">Blog</h1>
        <div class="flex flex-wrap -m-4">
          <NuxtLink
            v-for="post in page"
            :key="post.id"
            :to="{ name: 'blog-slug', params: { slug: post.slug } }"
            class="p-4 md:w-1/3"
          >
            <div
              class="h-full border-2 border-gray-200 border-opacity-60 rounded-lg overflow-hidden"
            >
              <nuxt-img
                provider="cloudinary"
                class="lg:h-48 md:h-36 w-full object-cover object-center"
                :src="post.image"
                alt="blog"
              />
              <div class="p-6">
                <h2
                  class="tracking-widest text-xs title-font font-medium text-gray-400 mb-1"
                >
                  {{ formatDate(post.createdAt) }}
                </h2>
                <h1 class="title-font text-lg font-medium text-gray-900 mb-3">
                  {{ post.title }}
                </h1>
                <p class="leading-relaxed mb-3">
                  {{ post.description }}
                </p>
                <div class="flex items-center flex-wrap">
                  <a class="inline-flex items-center md:mb-2 lg:mb-0"
                    >Leer más
                    <svg
                      class="w-4 h-4 ml-2"
                      viewBox="0 0 24 24"
                      stroke="currentColor"
                      stroke-width="2"
                      fill="none"
                      stroke-linecap="round"
                      stroke-linejoin="round"
                    >
                      <path d="M5 12h14"></path>
                      <path d="M12 5l7 7-7 7"></path>
                    </svg>
                  </a>
                </div>
              </div>
            </div>
          </NuxtLink>
        </div>
      </div>
    </section>
  </article>
</template>

<script>
export default {
  async asyncData({ $content }) {
    const page = await $content().fetch();

    return {
      page,
    };
  },
  methods: {
    formatDate(date) {
      const options = { year: "numeric", month: "long", day: "numeric" };
      return new Date(date).toLocaleDateString("es", options);
    },
  },
};
</script>
