<template>
  <div class="page-outer-container">
    <div class="title-section-outer-container">
      <div class="title-section-inner-container">
        <div class="title-section-left">
          <h2 class="title-section-title">{{ homepage.fields.pageTitle }}</h2>
          <h4 class="title-section-subtitle">{{ homepage.fields.pageText }}</h4>
        </div>
        <div class="title-section-right">
          <img
            :src="homepage.fields.heroImage.fields.file.url"
            class="title-section-image"
            alt=""
          >

        </div>

      </div>
    </div>
    <!-- <div class="blogposts-section-outer-container">
      <div class="blogposts-section-inner-container">
        <div class="blogposts-section-upper-third">
          <h3 class="blogposts-section-title">En son yazılar</h3>
          <button class="blogpost-button">Tüm yazılar</button>
        </div>
        <div class="blogposts-section-lower-third">
          <template v-for="blogpost in blogposts">
            <div
              :key="blogpost"
              class="blogpost-tile"
            >
              <h4 class="blogpost-title">{{ blogpost.fields.title }}</h4>
              <p class="blogpost-summary">{{ blogpost.fields.summary }}</p>
              <button class="blogpost-button">Okumaya devam et</button>
            </div>
          </template>
        </div>
      </div>
    </div> -->
  </div>

</template>

<script>
import { createClient } from '@/plugins/contentful.js'
const client = createClient()
export default {
  transition: 'page',
  asyncData({ env }) {
    return Promise.all([
      // fetch all blog posts sorted by creation date
      client.getEntries({
        content_type: 'homepage',
        order: '-sys.createdAt'
      }),
      client.getEntries({
        content_type: 'blogPost',
        order: '-sys.createdAt'
      })
    ])
      .then(([homepagePosts, blogPosts]) => {
        // return data that should be available
        // in the template
        return {
          homepage: homepagePosts.items[0],
          blogposts: blogPosts.items.slice(0, 3)
        }
      })
      .catch(console.error)
  }
}
</script>

<style lang="scss" scoped>
h1,
h2,
h3,
h4,
p {
  font-family: 'Dosis', sans-serif;
}
.page-outer-container {
  width: 100%;
}
.title-section-outer-container {
  width: 100%;
  height: calc(100vh - 80px);
  background: #f2ebe3;
  display: flex;
  justify-content: center;
  .title-section-inner-container {
    position: relative;
    width: 1100px;
    height: 100%;
    padding: 30px;
    /* border: 1px dashed grey; */
    display: flex;
    .title-section-left {
      display: flex;
      flex-direction: column;
      justify-content: center;
      width: 50%;
      height: 100%;
      .title-section-title {
        font-size: 3rem;
        font-weight: 600;
      }
      .title-section-subtitle {
        font-size: 1rem;
        color: #ca6c73;
      }
    }
    .title-section-right {
      position: relative;
      display: flex;
      justify-content: center;
      align-items: center;
      width: 50%;
      height: 100%;
      .title-section-image {
        width: 80%;
        box-shadow: -10px -10px 0 0 white, 10px 10px 0 0 #ca6c73;
      }
    }
  }
}
.blogposts-section-outer-container {
  width: 100%;
  height: calc(100vh - 80px);
  background: $primary;
  display: flex;
  justify-content: center;
  .blogposts-section-inner-container {
    position: relative;
    width: 1100px;
    height: 100%;
    padding: 30px;
    border: 1px dashed lightgrey;
    display: flex;
    flex-direction: column;
    .blogposts-section-upper-third {
      height: calc(100% / 3);
      width: 100%;
      display: flex;
      flex-direction: column;
      align-items: flex-end;
      /* background: rgba(0, 0, 0, 0.1); */
      .blogposts-section-title {
        color: #f2ebe3;
        font-size: 3rem;
        font-weight: 600;
      }
      button {
        width: initial;
      }
    }
    .blogposts-section-lower-third {
      position: relative;
      height: calc((100% / 3) * 2);
      width: 100%;
      /* background: rgba(0, 0, 0, 0.3); */
      display: flex;
      justify-content: space-between;
      align-items: center;
      .blogpost-tile {
        width: 30%;
        height: 90%;
        /* background: rgba(255, 255, 255, 0.2); */
        display: flex;
        flex-direction: column;
        justify-content: space-around;
        .blogpost-title {
          font-size: 1.5rem;
          font-weight: 600;
          color: white;
        }
        .blogpost-summary {
          font-size: 1rem;
          color: white;
        }
      }
    }
    .blogpost-button {
      width: 100%;
      height: 50px;
      border: 2px solid white;
      border-radius: 2px;
      font-family: 'Dosis', sans-serif;
      font-size: 1.5rem;
      text-align: center;
      color: white;
      background: none;
      cursor: pointer;
      transition: 0.2s;
      &:hover {
        background: rgba(255, 255, 255, 0.1);
      }
    }
  }
}
</style>
