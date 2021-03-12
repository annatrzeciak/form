<template>
  <div class="contact-form">
    <main-contact-view />
  </div>
</template>

<script>
import MainContactView from './MainContactView'
export default {
  name: 'ContactForm',
  components: { MainContactView }
}
</script>

<style scoped lang="scss">
.contact-form {
  border: 1px solid #491989;
  border-radius: 3px;
  padding: 50px;
  @media (max-width: 968px) {
    margin-right: 20px;
    margin-left: 20px;
  }
  @media (max-width: 720px) {
    padding: 25px;
  }
}
</style>
<style lang="scss">
.contact-form {
  h2 {
    text-align: center;
    color: #491989;
    margin-bottom: 0;
    font-size: 22px;
  }
  h3 {
    margin-top: 0;
    text-align: center;
    color: #491989;
    font-weight: 300;
    font-size: 22px;
  }
}
</style>
