<template>
  <div class="page-outer-container">
    <h1>Hakkımızda</h1>
    <div
      v-for="aboutText in aboutTexts"
      :key="aboutText.fields.order"
      class="about-section-outer-container"
    >
      <div class="about-section-inner-container">
        <h1>{{ aboutText.fields.title }}</h1>
        <p>{{ aboutText.fields.text }}</p>

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
      // fetch the owner of the blog
      // fetch all blog posts sorted by creation date
      client.getEntries({
        content_type: 'about',
        order: 'fields.order'
      })
    ])
      .then(([aboutTexts]) => {
        // return data that should be available
        // in the template
        return {
          aboutTexts: aboutTexts.items
        }
      })
      .catch(console.error)
  }
}
</script>

<style lang="scss" scoped>
.page-outer-container {
  width: 1100px;
  .about-section-outer-container {
    width: 100%;
    height: 500px;
    background: #f2ebe3;
    display: flex;
    justify-content: center;
    margin: 30px 0;
    .about-section-inner-container {
      position: relative;
      width: 1100px;
      height: 100%;
      padding: 30px;
      border: 1px dashed grey;
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
    }
  }
}
</style>
