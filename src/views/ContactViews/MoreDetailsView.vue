<template>
  <div class="contact-form--more-details-view">
    <form class="form" @submit.prevent="submit">
      <contact-form>
        <template v-slot:header>
          <h2>
            <strong>Czy chciałbyś dodać jeszcze coś od siebie?</strong>
          </h2>
          <div v-if="sendingError" class="error">{{ sendingError }}</div>
        </template>
        <template v-slot:content>
          <label>
            Treść wiadomości (niewymagane)
            <textarea v-model="form.description" />
          </label>
          <label class="contact-form__agree">
            <input v-model="form.agree" type="checkbox" />
            <span>
              Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do
              eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut
              enim ad minim veniam, quis nostrud exercitation ullamco laboris
              nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in
              reprehenderit in voluptate velit esse cillum dolore eu fugiat
              nulla pariatur. Excepteur sint occaecat cupidatat non proident,
              sunt in culpa qui officia deserunt mollit anim id est laborum.
              <span class="error" v-if="submitError && !form.agree"
                ><br />Zgoda jest wymagana
              </span>
            </span>
          </label>
        </template>
        <template v-slot:footer>
          <button type="button" class="outline" @click="$emit('prev')">
            WSTECZ
          </button>
          <button :disabled="sending" type="submit">
            {{ sending ? "WYSYŁANIE..." : "WYŚLIJ" }}
          </button>
        </template>
      </contact-form>
    </form>
  </div>
</template>

<script>
import ContactForm from "../../components/ContactForm";
import axios from "axios";

export default {
  name: "MoreDetailsView",
  components: { ContactForm },

  props: {
    data: { type: Object }
  },
  data: function () {
    return {
      form: {
        description: "",
        agree: false
      },
      submitError: false,
      sendingError: "",
      sending: false
    };
  },
  methods: {
    async submit () {
      if (!this.form.agree) {
        this.submitError = true;
        return;
      }
      this.sending = true;
      this.sendingError = null;

      try {
        await axios.post(`${process.env.VUE_APP_API_URL}/contact`, {
          ...this.data,
          more: this.form.description
        });
        this.$emit("next");
      } catch (e) {
        console.error(e);
        this.sendingError = e.message;
      } finally {
        this.sending = false;
      }
    }
  }
};
</script>

<style lang="scss" scoped>
.contact-form {
}
</style>
