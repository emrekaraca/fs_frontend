
<template>
  <div class="page-outer-container">
    <div class="page-inner-container">
      <h1>Blog</h1>
      <h3>Tüm Konular</h3>
      <br>
      <template v-for="post in posts">
        <blog-entry
          :key="post.fields.title"
          :post="post"
        />

      </template>
      <button
        v-if="($route.query.page || 1) > 1"
        @click="previousPage()"
      >Previous Page</button>
      <h3>Page {{ $route.query.page || 1 }}/{{ Math.ceil(totalPosts/pageItems) }}</h3>
      <button
        v-if="($route.query.page || 1) < Math.ceil(totalPosts/pageItems)"
        @click="nextPage()"
      >Next Page</button>
    </div>
  </div>

</template>

<script>
import BlogEntry from './BlogEntry'
import { createClient } from '@/plugins/contentful.js'
const client = createClient()
export default {
  name: 'Home',
  components: {
    BlogEntry
  },
  data() {
    return {
      pageItems: 3
    }
  },
  methods: {
    nextPage() {
      let currentPage = this.$route.query.page || 1
      this.$router.push({
        path: '/blog',
        query: { page: ++currentPage }
      })
    },
    previousPage() {
      let currentPage = this.$route.query.page || 1
      this.$router.push({
        path: '/blog',
        query: { page: --currentPage }
      })
    }
  },
  asyncData({ query, env }) {
    let skipNumber = (query.page - 1 || 0) * 3
    console.log(query, skipNumber)
    return Promise.all([
      // fetch the owner of the blog
      // fetch all blog posts sorted by creation date
      client.getEntries({
        content_type: env.CTF_BLOG_POST_TYPE_ID,
        order: '-fields.publishDate',
        limit: 3,
        skip: skipNumber
      })
    ])
      .then(([posts]) => {
        // return data that should be available
        // in the template
        console.log(posts)
        return {
          totalPosts: posts.total,
          posts: posts.items
        }
      })
      .catch(console.error)
  },
  watchQuery: ['page']
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
