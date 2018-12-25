<template>
  <div class="page-outer-container">
    <div class="page-section-outer-container">
      <div class="page-section-inner-container">
        <h2 class="section-title">{{ post.fields.pageTitle }}</h2>
        <p class="section-subtitle">{{ post.fields.pageText }}</p>
        <!-- <img
        :src="post.fields.heroImage.fields.file.url"
        alt=""
      > -->

      </div>
    </div>
  </div>

</template>

<script>
import { createClient } from '@/plugins/contentful.js'
const client = createClient()
export default {
  asyncData({ env }) {
    return Promise.all([
      // fetch all blog posts sorted by creation date
      client.getEntries({
        content_type: 'homepage',
        order: '-sys.createdAt'
      })
    ])
      .then(([posts]) => {
        // return data that should be available
        // in the template
        return {
          post: posts.items[0]
        }
      })
      .catch(console.error)
  }
}
</script>

<style lang="scss" scoped>
.page-outer-container {
  width: 100%;
}
.page-section-outer-container {
  width: 100%;
  height: 600px;
  background: #f2ebe3;
  display: flex;
  justify-content: center;
  .page-section-inner-container {
    width: 1100px;
    height: 100%;
    padding: 30px;
    border: 1px dashed grey;
  }
}
.section-title {
  font-size: 3rem;
  font-weight: 600;
  font-family: 'Dosis', sans-serif;
}
.section-subtitle {
  font-size: 1rem;
  font-family: 'Dosis', sans-serif;
  color: #ca6c73;
}
</style>
