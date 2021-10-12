<template>
  <div class="container box">
    <h2 class="subtitle is-2 has-text-info">{{ post.title }}</h2>
    <nuxt-content :document="post" />
    <nav class="pagination is-justify-content-center">
      <NuxtLink v-if="post.previous" class="pagination-previous" :to="{path: post.previous}">Previous</NuxtLink>
      <NuxtLink class="pagination-previous" to="/">Home</NuxtLink>
      <NuxtLink v-if="post.next" class="pagination-previous" :to="{path: post.next}">Next</NuxtLink>
    </nav>
  </div>
</template>

<script>
export default {
  async asyncData({ $content, params, error }) {
    let post;
    try {
      post = await $content("blog", params.slug).fetch();
      
    } catch (e) {
      error({ message: "Blog Post not found" });
    }

    return {
      post,
    };
  },
};
</script>
