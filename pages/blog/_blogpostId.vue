<template>
  <div class="blog-outer-container">
    <br>
    <h1>{{ post.fields.title }}</h1>
    <br>
    <h4>Tarih: {{ post.fields.publishDate.slice(0,10) }}</h4>
    <br>
    <p v-html="docToString(post.fields.text)" />
  </div>
</template>

<script>
import { BLOCKS } from '@contentful/rich-text-types'
import { documentToHtmlString } from '@contentful/rich-text-html-renderer'
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
  data() {
    return {
      docToStringOptions: {
        renderNode: {
          [BLOCKS.EMBEDDED_ASSET]: node =>
            `<img src="${node.data.target.fields.file.url}" alt="${
              node.data.target.fields.description
            }" />`
          // ['BLOCKS.EMBEDDED_ASSET']: node => `<img src='${node}' alt='' />`
        }
      }
    }
  },
  methods: {
    docToString(input) {
      return documentToHtmlString(input, this.docToStringOptions)
    }
  }
}
</script>

<style lang="scss" scoped>
.blog-outer-container {
  width: 1100px;
}
.text--bold {
  font-weight: 800;
}
.text--italic {
  font-style: italic;
}
</style>
