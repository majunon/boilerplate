<template>
  <div>
    <h1>Nuxt + Netlify CMS Boilerplate</h1>
    <h2>an how-to guide</h2>
    <li v-for="post of posts" :key="post.slug">
      <NuxtLink :to="post.slug">
        {{ post.title }}
      </NuxtLink>
    </li>
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
