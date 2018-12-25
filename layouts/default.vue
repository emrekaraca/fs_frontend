<template>
  <div class="page-container has-background-light">
    <nav-bar />
    <div style="height: 500px">space</div>
    <footer-bar />

    <!-- <section class="main-content columns">
      <div class="column is-12 has-background-light">
        <nuxt />
      </div>
    </section> -->
  </div>
</template>

<script>
import NavBar from '@/components/NavBar'
import FooterBar from '@/components/Footer'
export default {
  components: {
    NavBar,
    FooterBar
  },
  data() {
    return {}
  }
}
</script>

<style lang="scss" scoped>
.page-container {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  align-items: center;
}
.page-title {
  font-size: 2rem;
}
</style>
