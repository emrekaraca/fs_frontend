<template>
  <div>
    <h1>Blog</h1>
    <br>
    <div class="columns is-multiline">
      <div
        v-for="post in posts"
        :key="post.fields.title"
        class="column is-6-desktop is-12-mobile"
      >
        <h2 class="is-size-4">{{ post.fields.title }}</h2>
        <img
          :src="`${post.fields.image.fields.file.url}?w=400&h=200`"
          :alt="post.fields.image.fields.description"
        >
        <p>{{ post.fields.summary }}</p>

      </div>
    </div>
  </div>

</template>

<script>
console.log(process.env)
import { createClient } from '@/plugins/contentful.js'
const client = createClient()
export default {
  name: 'Home',
  data() {
    return {}
  },
  asyncData({ env }) {
    return Promise.all([
      // fetch the owner of the blog
      // fetch all blog posts sorted by creation date
      client.getEntries({
        content_type: env.CTF_BLOG_POST_TYPE_ID,
        order: '-sys.createdAt'
      })
    ])
      .then(([posts]) => {
        // return data that should be available
        // in the template
        return {
          posts: posts.items
        }
      })
      .catch(console.error)
  }
}
</script>
