
<template>
  <div class="page-outer-container">
    <div class="page-inner-container">
      <h1>Blog</h1>
      <br>
      <template v-for="post in posts">
        <blog-entry
          :key="post.fields.title"
          :post="post"
        />

      </template>
    </div>
  </div>

</template>

<script>
import BlogEntry from '@/components/BlogEntry'
import { createClient } from '@/plugins/contentful.js'
const client = createClient()
export default {
  name: 'Home',
  components: {
    BlogEntry
  },
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

<style lang="scss" scoped>
.page-outer-container {
  width: 100%;
  display: flex;
  justify-content: center;
  .page-inner-container {
    width: 1100px;
  }
}
</style>
