<template>
  <div class="contact-page">
    <header>
      <div>
        <h1>
          <strong>szukam</strong><br />
          kreatora
        </h1>
      </div>
      <div>
        <img src="/iPad.png" alt="IPad - aplikacja" title="Kreator - IPad" />
      </div>
    </header>
    <section class="contact-form-section">
      <main-contact-view />
    </section>
  </div>
</template>

<script>
import MainContactView from './MainContactView'
export default {
  name: 'Contact',
  components: { MainContactView }
}
</script>

<style lang="scss" scoped>
.contact-page {
  header {
    max-width: 100%;
    width: calc(100vw - (100vw - 968px) / 2);
    margin-left: auto;
    margin-right: 0;
    display: flex;
    position: relative;
    @media (max-width: 678px) {
      flex-direction: column;
    }
    div {
      float: left;
      height: 462px;
      box-sizing: border-box;
      width: 50%;

      @media (max-width: 968px) {
        height: auto;
      }
      @media (max-width: 678px) {
        width: 100%;
      }
      &:first-of-type {
        padding-left: 58px;
        padding-top: 50px;
        background-image: url("/top_bg2.jpeg");
        background-size: cover;
        background-position: center right;
        display: flex;
        align-items: flex-end;
        @media (max-width: 678px) {
          padding-left: 25px;
        }
      }
      &:nth-of-type(2) {
        padding-top: 50px;
        background-image: url("/top_bg1.jpeg");
        background-size: cover;
        background-position: center left;
        @media (max-width: 1100px) {
          display: flex;
          justify-content: center;
        }
        img {
          position: absolute;
          left: calc(50% - 210px);
          bottom: 50px;
          @media (max-width: 1100px) {
            position: static;
            margin-bottom: 50px;
            max-width: 90%;
          }
        }
      }
      h1 {
        font-size: 65px;
        font-weight: normal;
        color: #fff;
        @media (max-width: 678px) {
          font-size: 50px;
        }
      }
    }
  }
  .contact-form-section {
    margin: 130px auto;
    max-width: 968px;
    width: 100%;
  }
}
</style>
