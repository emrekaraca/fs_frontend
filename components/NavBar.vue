<template>
  <div class="navbar-outer-container">
    <div class="navbar-logo">
      <img
        src="@/assets/FS_logo.svg"
        alt="FS-logos"
        class="navbar-logo-image"
      >
      <p class="navbar-logo-title">FITOSOFİA</p>
    </div>
    <div class="navbar-menu">
      <nuxt-link
        :class="$route.name==='index'?'selected':''"
        to="/"
      ><span>Anasayfa</span></nuxt-link>
      <nuxt-link
        :class="$route.name==='blog'?'selected':''"
        to="/blog"
      ><span>Blog</span></nuxt-link>
      <nuxt-link
        :class="$route.name==='academy'?'selected':''"
        to="/academy"
      ><span>Akademi</span></nuxt-link>
      <nuxt-link
        :class="$route.name==='about'?'selected':''"
        to="/about"
      ><span>Hakkımızda</span></nuxt-link>
    </div>
  </div>
</template>

<style lang="scss" scoped>
@import './../assets/buefy_custom.scss';
.navbar-outer-container {
  width: 100%;
  height: 80px;
  background: $light;
  box-shadow: 0px 2px 4px 0px #afa2a2;
  display: flex;
  justify-content: space-between;
  box-sizing: border-box;
  padding: 0 15px;
  .navbar-logo {
    height: 100%;
    display: flex;
    align-items: center;
    .navbar-logo-image {
      height: 50px;
    }
    .navbar-logo-title {
      font-family: 'Dosis', sans-serif;
      font-weight: 500;
      font-size: 1.75rem;
      margin-left: 10px;
      letter-spacing: 0.25rem;
      color: $primary;
    }
  }
  .navbar-menu {
    display: flex;
    justify-content: flex-end;
    align-items: center;
    a {
      height: 100%;
      display: flex;
      align-items: center;
      font-family: 'Dosis', sans-serif;
      font-weight: 800;
      font-size: 1.25rem;
      color: $primary;
      margin: 0 10px;
      cursor: pointer;
      transition: 0.2s;
      &:after {
        transition: 0.3s;
        position: absolute;
        content: '';
        width: 100%;
        height: 100%;
        border-top: 5px solid #ca6c73;
        opacity: 0;
      }
      &.selected {
        color: #ca6c73;
        position: relative;
        &:after {
          opacity: 1;
        }
      }
      &:hover {
        color: #ca6c73;
      }
    }
  }
}
</style>
