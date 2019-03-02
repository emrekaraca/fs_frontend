<template>
  <div class="page-outer-container">
    <h1>Hizmetler</h1>
    <div
      v-for="service in services"
      :key="service.fields.order"
      class="service-section-outer-container"
    >
      <div class="service-section-inner-container">
        <TitleBox level="1">{{ service.fields.title }}</TitleBox>
        <p>{{ service.fields.text }}</p>

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
  .service-section-outer-container {
    width: 100%;
    background: #f2ebe3;
    display: flex;
    justify-content: center;
    margin: 30px 0;
    .service-section-inner-container {
      position: relative;
      height: 100%;
      padding: 20px;
      border: 1px dashed grey;
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
    }
  }
}
</style>
