---
title: 6- Add a blog list page
date: 2021-10-12T07:50:02.194Z
description: Woot !
next: 7-Create_a_template_to_visualize_a_blog_post
previous: 5-Configure_Identity_OAuth_on_Netlify
---

install nuxt/content :
`npm i @nuxt/content`

use this template to display a list of blog titles :

```
<template>
  <div>
    <h1>Nuxt + Netlify CMS Boilerplate</h1>
    <h2>an how-to guide</h2>
    <li v-for="post of posts" :key="post.slug">
      <NuxtLink :to="post.slug">{{ post.title }}</NuxtLink>
    </li>
  </div>
</template>
```
