<template>
  <div class="contact-form--thank-you-view">
    <contact-form>
      <template v-slot:content>
        <div class="message">
          <img
            src="/check.png"
            alt="Thank you"
            title="Thank for your details"
          />
          <h2>
            <strong>Dziękujemy za wysłanie<br>oraz przesłanie formularza.</strong>
          </h2>
          <h3>
            Wkrótce skontaktujemy się z Tobą,<br>w celu omówienia szczegółów.
          </h3>
          <button @click="redirectToHome">Wróć do strony głównej</button>
        </div>
      </template>
    </contact-form>
  </div>
</template>

<script>
import ContactForm from "../../components/ContactForm";

export default {
  name: "ThankYouView",
  components: { ContactForm },
  data: function () {
    return {};
  },
  methods: {
    redirectToHome () {
      window.location.href = "/";
    }
  }
};
</script>

<style lang="scss" scoped>
.contact-form {
  &--thank-you-view {
     .message {
      display: flex;
      justify-content: center;
      align-items: center;
       flex-direction: column;
       height: 100%;
       margin-right: auto;
       margin-left: auto;
      button {
        width: 214px;
      }
       img{
         margin-top: 72px;
         margin-bottom: 45px;
       }
       h2{
         margin-bottom: 28px;
       }
       h3{
         margin-bottom: 85px;
       }
    }
  }
}
</style>
