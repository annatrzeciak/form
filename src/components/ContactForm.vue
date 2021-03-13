<template>
  <div class="contact-form">
    <div class="contact-form__header">
      <slot name="header"></slot>
    </div>
    <div class="contact-form__content">
      <slot name="content"></slot>
    </div>
    <div class="contact-form__footer">
      <slot name="footer"></slot>
    </div>
  </div>
</template>

<script>
export default {
  name: 'ContactForm'
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
  &__header {
    text-align: center;
    color: #491989;

    h2 {
      margin-bottom: 0;
      font-size: 22px;
      font-weight: 300;
    }

    h3 {
      margin-top: 0;
      font-weight: 300;
      font-size: 22px;
    }
    @media (max-width: 720px) {
      h2,h3{
        font-size: 18px;
      }
    }
  }
}
</style>
