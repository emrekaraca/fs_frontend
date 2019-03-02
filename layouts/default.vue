<template>
  <div class="page-container">
    <nav-bar />
    <div class="main-grid">
      <div class="main-content">
        <nuxt />
      </div>
    </div>
    <footer-bar />
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
  background: $light;
}
.page-title {
  font-size: 2rem;
}
.main-grid {
  width: 100%;
  height: 100%;
  display: flex;
  .main-content {
    min-height: calc(100vh - #{$navbar-height} - 200px);
    width: 100%;
    height: 100%;
  }
}
@media #{$bp-l} {
  .main-grid {
    display: grid;
    grid-template: $main-grid;
    .main-content {
      grid-area: content;
    }
  }
}
</style>
