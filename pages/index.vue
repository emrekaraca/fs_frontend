<template>
  <div class="columns is-multiline">
    <div class="column is-12 page-section">
      <div
        class="columns"
        style="height: 100%"
      >
        <div class="column is-12-mobile is-10-desktop is-offset-1-desktop is-8-widescreen is-offset-2-widescreen">
          <div
            class="columns is-vcentered"
            style="height: 100%"
          >
            <div class="column is-6">
              <h2 class="section-title">{{ post.fields.pageTitle }}</h2>
              <p class="section-subtitle">{{ post.fields.pageText }}</p>
            </div>
            <div class="column is-6">
              <div style="width: 400px; height: 400px">
                <img
                  :src="post.fields.heroImage.fields.file.url"
                  alt=""
                >
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
    <div class="column is-12 page-section has-background-primary has-text-white">
      <div class="columns">
        <div class="column is-12-mobile is-10-desktop is-offset-1-desktop is-8-widescreen is-offset-2-widescreen">
          <p>TEST</p>
        </div>
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
.hero-container {
  background: red;
  width: 100%;
}
.page-section {
  height: 600px;
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
