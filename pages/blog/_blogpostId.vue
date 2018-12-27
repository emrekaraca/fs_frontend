<template>
  <div>
    <h1>This is blog post {{ post.fields.title }}</h1>
    <h4>Date: {{ post.fields.publishDate.slice(0,10) }}</h4>
    <template v-for="(paragraph, index) in post.fields.text.content">
      <template v-if="paragraph.nodeType === 'paragraph'">
        <p :key="index">
          <template v-for="partial in paragraph.content">
            <span
              :class="partial.marks.map(mark => `text--${mark.type}`).join(' ')"
              :key="partial.value"
            >{{ partial.value }}</span>
          </template>
        </p>
      </template>
      <template v-else-if="paragraph.nodeType === 'heading-1'">
        <h4 :key="index">
          <template v-for="partial in paragraph.content">
            <span
              :class="partial.marks.map(mark => `text--${mark.type}`).join(' ')"
              :key="partial.value"
            >{{ partial.value }}</span>
          </template>
        </h4>
      </template>
      <template v-else-if="paragraph.nodeType === 'heading-2'">
        <h5 :key="index">
          <template v-for="partial in paragraph.content">
            <span
              :class="partial.marks.map(mark => `text--${mark.type}`).join(' ')"
              :key="partial.value"
            >{{ partial.value }}</span>
          </template>
        </h5>
      </template>
      <template v-else-if="paragraph.nodeType === 'embedded-asset-block'">
        <img
          :key="index"
          :src="`${paragraph.data.target.fields.file.url}`"
          :alt="paragraph.data.target.fields.description"
        >
      </template>
    </template>
  </div>
</template>

<script>
import { createClient } from '@/plugins/contentful.js'
const client = createClient()

export default {
  asyncData({ params }) {
    return Promise.all([
      // fetch the owner of the blog
      // fetch all blog posts sorted by creation date
      client.getEntries({
        content_type: 'blogPost',
        'fields.slug[match]': params.blogpostId,
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
  },
  computed: {
    // paragraphs() {
    //   return this.post.text.content
    //   // .filter(p => p.nodeType === 'paragraph')
    //   // .map(p => p.content[0].value)
    // }
  }
}
</script>

<style lang="scss" scoped>
.text--bold {
  font-weight: 800;
}
.text--italic {
  font-style: italic;
}
</style>
