<template>
  <div class="container box">
    <h1 class="title is-1 has-text-primary">Nuxt + Netlify CMS Boilerplate</h1>
    <h2 class="subtitle is-2 has-text-info">an how-to guide</h2>
    <div v-for="post of posts" :key="post.slug" class="box">
      <NuxtLink :to="post.slug" class="has-text-black">
        {{ post.title }}
      </NuxtLink>
    </div>
  </div>
</template>

<script>
export default {
  async asyncData({ $content }) {
    const posts = await $content("blog").fetch();
    posts.sort((a,b) => {
      if(a.slug < b.slug){return -1;}
      else{return 1;}
    });
    return {
      posts,
    };
  },
  head() {
    return {
      script: [{ src: 'https://identity.netlify.com/v1/netlify-identity-widget.js' }],
    };
  },
};
</script>

<style scoped>
  h1,h2{
    text-align: center;
  }
</style>
