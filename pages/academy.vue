<template>
  <div class="page-outer-container">
    <h1>Akademi</h1>
    <div
      v-for="course in courses"
      :key="course.fields.order"
      class="academy-section-outer-container"
    >
      <div class="academy-section-inner-container">
        <h1>{{ course.fields.title }}</h1>
        <p v-html="docToString(course.fields.text)" />

      </div>
    </div>

  </div>
</template>

<script>
import { documentToHtmlString } from '@contentful/rich-text-html-renderer'
import { createClient } from '@/plugins/contentful.js'
const client = createClient()
export default {
  asyncData({ env }) {
    return Promise.all([
      // fetch the owner of the blog
      // fetch all blog posts sorted by creation date
      client.getEntries({
        content_type: 'courseTypes'
      })
    ])
      .then(([courses]) => {
        // return data that should be available
        // in the template
        return {
          courses: courses.items
        }
      })
      .catch(console.error)
  },
  methods: {
    docToString(input) {
      return documentToHtmlString(input)
    }
  }
}
</script>

<style lang="scss" scoped>
.page-outer-container {
  width: 1100px;
  .academy-section-outer-container {
    width: 100%;
    height: 500px;
    background: #f2ebe3;
    display: flex;
    justify-content: center;
    margin: 30px 0;
    .academy-section-inner-container {
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
