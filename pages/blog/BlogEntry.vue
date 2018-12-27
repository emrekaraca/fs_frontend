<template>
  <b-container class="blog-entry-outer-container">
    <b-row>
      <b-col cols="7">
        <div class="blog-entry-preview-image">
          <img
            :src="`${post.fields.image.fields.file.url}?fit=fill&w=400&h=300`"
            alt="asd"
          >
        </div>
      </b-col>
      <b-col
        cols="5"
        class="blog-entry-info"
      >
        <h2 class="blog-entry-title">{{ post.fields.title }}</h2>
        <p class="blog-entry-date">{{ transformDate(post.fields.publishDate) }}</p>
        <p class="blog-entry-summary">{{ post.fields.summary }}</p>
        <nuxt-link
          :to="`/blog/${post.fields.slug}`"
          class="blog-entry-button"
        >Okumaya devam et</nuxt-link>
      </b-col>
    </b-row>
  </b-container>

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
  margin: 20px 0;
  .blog-entry-info {
    display: flex;
    flex-direction: column;
    justify-content: center;
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
.blog-entry-preview-image {
  width: 100%;
  padding-top: calc(100% / 16 * 9);
  /* background: $light; */
  border: 5px solid $primary;
  box-sizing: border-box;
  img {
    position: absolute;
    top: 50%;
    left: 50%;
    width: 400px;
    transform: translate(-50%, -50%);
  }
}
</style>
