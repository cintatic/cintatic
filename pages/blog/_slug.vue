<template>
  <div class="container md:w-3/4 md:mx-auto">
    <br />
    <NuxtLink
      class="mt-rounded-lg bg-gray-100 active:shadow ml-8 p-2"
      to="/blog"
    >
      <font-awesome-icon :icon="['fas', 'arrow-left']" />
      Regresar al blog
    </NuxtLink>
    <h1 class="text-6xl mt-8 md:mt-8 mx-8 text-left">
      {{ post.title }}
    </h1>
    <div class="ml-8 mt-4 text-left">
      <p>{{ formatDate(post.createdAt) }}</p>
    </div>
    <div class="mx-8 my-8 border-t-2 pt-8 border-gray-300">
      <nuxt-content :document="post" />
      <NuxtImg
        class="rounded-lg m-4 mx-auto"
        provider="cloudinary"
        :src="post.image"
        width="800"
        height="500"
        format="webp"
      />
    </div>
  </div>
</template>

<script>
export default {
  async asyncData({ $content, params }) {
    const post = await $content(params.slug).fetch()
    return {
      post,
    }
  },
  methods: {
    formatDate(date) {
      const options = { year: 'numeric', month: 'long', day: 'numeric' }
      return new Date(date).toLocaleDateString('es', options)
    },
  },
}
</script>
