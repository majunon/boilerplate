---
title: 7- Create a template to visualize a blog post
date: 2021-10-12T07:50:02.194Z
description: Woot !
next: 0
previous: 6-Add_a_blog_list_page
---

Create a file named \_slug.vue in pages/ and add this content :

```
<template>
  <div>
    <h2>{{ post.title }}</h2>
    <nuxt-content :document="post" />
  </div>
</template>

<script>
export default {
  async asyncData({ $content, params, error }) {
    let post;
    try {
      post = await $content("blog", params.slug).fetch();
      // OR const article = await $content(`articles/${params.slug}`).fetch()
    } catch (e) {
      error({ message: "Blog Post not found" });
    }

    return {
      post,
    };
  },
};
</script>
```
