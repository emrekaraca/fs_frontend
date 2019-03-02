<template>
  <div class="navbar-outer-container">
    <div class="navbar-inner-container">
      <div class="navbar-logo">
        <img
          src="@/assets/FS_logo.svg"
          alt="FS-logos"
          class="navbar-logo-image"
        >
        <nuxt-link
          to="/"
          class="navbar-logo-title"
        >FİTOSOFİA</nuxt-link>
      </div>
      <div class="navbar-menu">
        <nuxt-link
          :class="$route.name==='index'?'selected':''"
          to="/"
        ><span>Anasayfa</span></nuxt-link>
        <nuxt-link
          :class="$route.path.split('/')[1]==='blog'?'selected':''"
          to="/blog"
        ><span>Yazılar</span></nuxt-link>
        <nuxt-link
          :class="$route.name==='services'?'selected':''"
          to="/services"
        ><span>Hizmetler</span></nuxt-link>
        <nuxt-link
          :class="$route.name==='calendar'?'selected':''"
          to="/calendar"
        ><span>Takvim</span></nuxt-link>
        <nuxt-link
          :class="$route.name==='academy'?'selected':''"
          to="/academy"
        ><span>Akademi</span></nuxt-link>
        <nuxt-link
          :class="$route.name==='shop'?'selected':''"
          to="/shop"
        ><span>Shop</span></nuxt-link>
        <nuxt-link
          :class="$route.name==='about'?'selected':''"
          to="/about"
        ><span>Hakkımızda</span></nuxt-link>
      </div>
      <div class="navbar-burger">
        <div
          :class="['menu-burger', mobileMenuOpen ? 'close-btn' : '']"
          href="#menu"
          @click="toggleMobileMenu()"
        >
          <div class="top-line" />
          <div class="middle-line" />
          <div class="bottom-line" />
        </div>
      </div>
      <div :class="['navbar-mobile-menu', mobileMenuOpen ? 'mobile-menu-open' : '']">
        <nuxt-link
          :class="$route.name==='index'?'selected':''"
          to="/"
        ><span>Anasayfa</span></nuxt-link>
        <nuxt-link
          :class="$route.path.split('/')[1]==='blog'?'selected':''"
          to="/blog"
        ><span>Yazılar</span></nuxt-link>
        <nuxt-link
          :class="$route.name==='services'?'selected':''"
          to="/services"
        ><span>Hizmetler</span></nuxt-link>
        <nuxt-link
          :class="$route.name==='calendar'?'selected':''"
          to="/calendar"
        ><span>Takvim</span></nuxt-link>
        <nuxt-link
          :class="$route.name==='academy'?'selected':''"
          to="/academy"
        ><span>Akademi</span></nuxt-link>
        <nuxt-link
          :class="$route.name==='shop'?'selected':''"
          to="/shop"
        ><span>Shop</span></nuxt-link>
        <nuxt-link
          :class="$route.name==='about'?'selected':''"
          to="/about"
        ><span>Hakkımızda</span></nuxt-link>

      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'NavBar',
  data() {
    return {
      mobileMenuOpen: false
    }
  },
  watch: {
    $route: function() {
      this.closeMobileMenu()
    }
  },
  methods: {
    toggleMobileMenu() {
      this.mobileMenuOpen = !this.mobileMenuOpen
    },
    closeMobileMenu() {
      this.mobileMenuOpen = false
    }
  }
}
</script>


<style lang="scss" scoped>
.navbar-outer-container {
  width: 100%;
  height: $navbar-height;
  display: grid;
  grid-template: $main-grid;
  background: $light;
  box-shadow: 0px 2px 4px 0px #afa2a2;
  box-sizing: border-box;
  z-index: 9999;
  margin-bottom: 20px;
  .navbar-inner-container {
    position: relative;
    grid-area: content;
    display: flex;
    justify-content: center;
    @media #{$bp-l} {
      justify-content: space-between;
    }
  }
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
  a {
    font-family: 'Dosis', sans-serif;
    font-weight: 800;
    font-size: 1.25rem;
    color: $primary;
    cursor: pointer;
    transition: 0.2s;
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
  .navbar-menu {
    position: relative;
    display: none;
    @media #{$bp-l} {
      display: flex;
    }
    justify-content: flex-end;
    align-items: center;
    a {
      position: relative;
      height: 100%;
      display: flex;
      align-items: center;
      margin: 0 10px;
      &:after {
        /* transition: 0.2s; */
        position: absolute;
        content: '';
        width: 100%;
        height: 100%;
        border-top: 5px solid #ca6c73;
        opacity: 0;
      }
      &.selected {
        &:after {
          opacity: 1;
        }
      }
    }
  }
}
$burger-width: 30px;
$burger-height: $burger-width / 3 * 2;
.navbar-burger {
  height: 100%;
  width: $burger-width;
  position: absolute;
  right: 10px;
  @media #{$bp-m} {
    right: 25px;
  }
  top: 0;
  display: flex;
  align-items: center;
  @media #{$bp-l} {
    display: none;
  }
}
.menu-burger {
  position: relative;
  width: $burger-width;
  height: $burger-height;
  cursor: pointer;
  [class$='-line'] {
    position: absolute;
    left: 0;
    width: 100%;
    height: $burger-height / 5;
    background-color: $primary;
    transition: 0.2s;
  }
  .top-line {
    top: 0;
  }
  .middle-line {
    top: 50%;
    transform: translateY(-50%);
  }
  .bottom-line {
    bottom: 0;
  }
  &.close-btn {
    .top-line {
      top: 50%;
      transform: rotate(45deg);
      transform-origin: center center;
    }
    .middle-line {
      opacity: 0;
    }
    .bottom-line {
      top: 50%;
      transform: rotate(-45deg);
      transform-origin: center center;
    }
  }
}
.navbar-mobile-menu {
  position: absolute;
  display: flex;
  opacity: 0;
  flex-direction: column;
  align-items: center;
  padding-top: 25px;
  box-sizing: border-box;
  top: 100%;
  left: 0;
  width: 100%;
  min-height: 0;
  height: 0;
  max-height: 0;
  transition: height 0.3s;
  transition: max-height 0.3s;
  transition: 0.3s;
  overflow: hidden;
  background-color: $light;
  &.mobile-menu-open {
    opacity: 1;
    height: calc(100vh - #{$navbar-height});
    max-height: calc(100vh - #{$navbar-height});
    min-height: 400px;
  }
  @media #{$bp-l} {
    display: none;
  }
  a {
    font-family: 'Dosis', sans-serif;
    font-weight: 800;
    font-size: 2rem;
    margin: 5px 0;
    color: $primary;
    cursor: pointer;
    transition: 0.2s;
    &.selected {
      border-bottom: 3px solid $red;
    }
  }
}
</style>
