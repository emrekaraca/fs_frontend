<template>
  <div class="page-outer-container">
    <div
      v-for="service in services"
      :key="service.fields.order"
      class="service-section-outer-container"
    >
      <div class="service-section-inner-container">
        <h1>{{ service.fields.title }}</h1>
        <p>{{ service.fields.text }}</p>

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
        content_type: 'service',
        order: 'fields.order'
      })
    ])
      .then(([services]) => {
        // return data that should be available
        // in the template
        return {
          services: services.items
        }
      })
      .catch(console.error)
  }
}
</script>

<style lang="scss" scoped>
.page-outer-container {
  width: 100%;
  .service-section-outer-container {
    width: 100%;
    height: 500px;
    background: #f2ebe3;
    display: flex;
    justify-content: center;
    margin: 30px 0;
    .service-section-inner-container {
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
