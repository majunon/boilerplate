<template>
  <div class="container box">
    <h2 class="subtitle is-2 has-text-info">{{ post.title }}</h2>
    <nuxt-content :document="post" />
    <nav class="pagination is-justify-content-center">
      <NuxtLink v-if="prev" class="pagination-previous" :to="{ path: prev.slug }">Previous</NuxtLink>
      <NuxtLink class="pagination-previous" to="/">Home</NuxtLink>
      <NuxtLink v-if="next" class="pagination-previous" :to="{ path: next.slug }">Next</NuxtLink>
    </nav>
  </div>
</template>

<script>
export default {
  async asyncData({ $content, params}) {
    const post = await $content("blog", params.slug).fetch();
    const [prev, next] = await $content("blog")
      .only(['title', 'slug'])
      .sortBy('title', 'asc')
      .surround(params.slug)
      .fetch();     
    return {
      post,
      prev,
      next
    };
  },
};
</script>
