<template>
  <div class="blog-outer-container">
    <div class="post-back-link">
      <a @click="$router.go(-1) ">&#8592; Geri git</a>
    </div>
    <br>
    <div class="post-header">
      <TitleBox level="1">
        {{ post.fields.title }}
      </TitleBox>
      <TitleBox level="4">
        {{ post.fields.publishDate.slice(0,10) }}
      </TitleBox>
    </div>
    <br>
    <br>
    <div
      class="post-content"
      v-html="docToString(post.fields.text)"
    />
  </div>
</template>

<script>
import TitleBox from '@/components/TitleBox'
import { BLOCKS } from '@contentful/rich-text-types'
import { documentToHtmlString } from '@contentful/rich-text-html-renderer'
import { createClient } from '@/plugins/contentful.js'
const client = createClient()

export default {
  components: {
    TitleBox
  },
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

<style lang="scss">
.blog-outer-container {
  margin: 20px;
}
.post-back-link {
  color: $primary;
}
.post-header {
  display: flex;
  flex-direction: column;
  align-items: center;
  @media #{$bp-l} {
    flex-direction: row;
    justify-content: space-between;
  }
}
.post-content {
  display: flex;
  flex-direction: column;
  align-items: center;
  p {
    width: 100%;
  }
  img {
    margin: 15px;
    box-shadow: -10px -10px 0 0 white, 10px 10px 0 0 $primary;
    max-width: 90%;
    height: auto;
    @media #{$bp-l} {
      max-width: 50%;
    }
  }
}
.text--bold {
  font-weight: 800;
}
.text--italic {
  font-style: italic;
}
</style>
