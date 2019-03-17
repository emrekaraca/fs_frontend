<template>
  <div class="footer-outer-container">
    <!-- <div class="footer-top-area">
      <div class="area-logo">
        <img
          src="@/assets/FS_logo_white.svg"
          alt="FS-logos"
          class="footer-logo-image"
        >
        <nuxt-link
          to="/"
          class="footer-logo-title"
        >FİTOSOFİA</nuxt-link>
      </div>
      <div class="area-links1">
        <h4>Linkler 1</h4>
        <ul>
          <li>Link</li>
          <li>Link</li>
          <li>Link</li>
        </ul>
      </div>
      <div class="area-links2">
        <h4>Linkler 2</h4>
        <ul>
          <li>Link</li>
          <li>Link</li>
          <li>Link</li>
        </ul>
      </div>
      <div class="area-newsletter">
        <h4>Newsletter</h4>
      </div>
    </div> -->
    <div class="footer-line" />
    <div class="footer-lower-area">
      <p>© {{ new Date().getFullYear() }} Şaduman Karaca</p>
      <div class="social-links">
        <img
          src="@/assets/facebook.png"
          alt="facebook"
        >
        <img
          src="@/assets/instagram.png"
          alt="instagram"
        >
        <img
          src="@/assets/youtube.png"
          alt="youtube"
        >
      </div>
    </div>
  </div>
</template>

<style lang="scss" scoped>
.footer-outer-container {
  width: 100%;
  background: $blue;
  color: white;
  display: flex;
  flex-direction: column;
  @media #{$bp-l} {
    display: grid;
    grid-template:
      '. content .' auto
      'line line line'
      '. lower .' auto /
      1fr minmax(100px, 970px) 1fr;
  }
  justify-content: center;
  .footer-top-area {
    width: 100%;
    padding: 35px 0 20px 0;
    @media #{$bp-l} {
      grid-area: content;
    }
    display: grid;
    grid-template:
      'logo links1 links2 contact' auto /
      30fr 20fr 20fr 40fr;
    [class^='area-'] {
      h4 {
        font-size: 18px;
        color: #fff;
        font-weight: 500;
      }
      ul {
        list-style: none;
        padding: 0;
        li {
          font-size: 16px;
          line-height: 2;
          color: #fff;
          opacity: 0.65;
          transition: opacity 0.3s;
          &:hover {
            opacity: 1;
          }
        }
      }
    }
    .area-logo {
      grid-area: logo;
      display: flex;
      flex-direction: column;
      align-items: center;
      .footer-logo-image {
        width: 60px;
      }
      .footer-logo-title {
        text-decoration: none;
        font-family: 'Dosis', sans-serif;
        color: white;
      }
    }
    .area-links1 {
      grid-area: links1;
    }
    .area-links2 {
      grid-area: links2;
    }
    .area-newsletter {
      grid-area: contact;
    }
  }
  .footer-line {
    grid-area: line;
    border-top: 1px solid $light;
  }
  .footer-lower-area {
    grid-area: lower;
    padding: 20px 30px;
    display: flex;
    justify-content: space-between;
    align-content: center;
    p {
      color: #fff;
      margin: 0;
    }
    .social-links {
      img {
        height: 20px;
        margin-left: 28px;
        cursor: pointer;
        transition: transform 0.3s;
        &:hover {
          transform: scale(1.2);
        }
      }
    }
  }
}
</style>
