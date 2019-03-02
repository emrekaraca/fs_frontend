<template>
  <div class="page-outer-container">
    <TitleBox level="1">Hakkımızda</TitleBox>
    <div
      v-for="aboutText in aboutTexts"
      :key="aboutText.fields.order"
      class="about-section-outer-container"
    >
      <div class="about-section-inner-container">
        <TitleBox level="1">{{ aboutText.fields.title }}</TitleBox>
        <p>{{ aboutText.fields.text }}</p>

      </div>
    </div>

  </div>
</template>

<script>
import TitleBox from '@/components/TitleBox'
import { createClient } from '@/plugins/contentful.js'
const client = createClient()
export default {
  components: {
    TitleBox
  },
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
  margin: 20px;
  .about-section-outer-container {
    width: 100%;
    background: #f2ebe3;
    display: flex;
    justify-content: center;
    margin: 30px 0;
    .about-section-inner-container {
      position: relative;
      width: 100%;
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
