<template>
  <div class="blog-entry-outer-container">
    <div class="blog-entry-preview-image">
      <img
        :src="`${post.fields.image.fields.file.url}?fit=fill&w=600&h=337`"
        alt="asd"
      >
    </div>
    <div class="blog-entry-info">
      <h2 class="blog-entry-title">{{ post.fields.title }}</h2>
      <p class="blog-entry-date">{{ transformDate(post.fields.publishDate) }}</p>
      <p class="blog-entry-summary">{{ post.fields.summary }}</p>
      <nuxt-link
        :to="`/blog/${post.fields.slug}`"
        class="blog-entry-button"
      >Okumaya devam et</nuxt-link>

    </div>

  </div>

</template>

<script>
export default {
  props: {
    post: {
      type: Object,
      default: () => null
    }
  },
  methods: {
    transformDate(inputDate) {
      const date = new Date(inputDate)
      return `${date.getDate()}.${date.getMonth() + 1}.${date.getFullYear()}`
    }
  }
}
</script>


<style lang="scss" scoped>
.blog-entry-outer-container {
  margin-bottom: 50px;
  display: grid;
  grid-template: 'image' auto 'text' auto / 1fr;
  .blog-entry-preview-image {
    grid-area: image;
    width: 100%;
    box-sizing: border-box;
    /* box-shadow: -10px -10px 0 0 white, 10px 10px 0 0 $primary; */
    /* padding: 0 50px; */
    margin-bottom: 25px;
    img {
      width: 100%;
      height: auto;
    }
  }
  .blog-entry-info {
    grid-area: text;
    display: flex;
    flex-direction: column;
    justify-content: center;
    margin: 0 30px;
    .blog-entry-title {
      font-weight: 900;
    }

    .blog-entry-button {
      border: 2px solid $primary;
      color: $primary;
      font-weight: 700;
      background: none;
      height: 50px;
      width: 100%;
      text-align: center;
      font-family: 'Dosis', sans-serif;
      font-size: 1.5rem;
    }
  }
}
</style>
