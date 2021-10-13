---
title: 8- Add navigations buttons
date: 2021-10-12T07:50:02.194Z
description: Woot !
---

For the home button, it's simple enough :

```
<NuxtLink to="/">Home</NuxtLink>
```

For the previous and next button, things are more complicated. We first need to fetch the url of the next and previous pages :

```
export default {
  async asyncData({ $content, params}) {
    const post = await $content("blog", params.slug).fetch();
    /* Add this part to get prev and next pages */
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
```

We then can use prev and next variables in the template code. Don't forget to test for the presence of a next or prev page :

```
<NuxtLink v-if="prev" class="pagination-previous" :to="{ path: prev.slug }">Previous</NuxtLink>
<NuxtLink v-if="next" class="pagination-previous" :to="{ path: next.slug }">Next</NuxtLink>
```
