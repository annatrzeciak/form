<template>
  <div class="contact-form--main-info-view">
    <form class="form" @submit.prevent="submit">
      <contact-form>
        <template v-slot:header>
          <h2>
            <strong>Wypełnij poniższy formularz, </strong> <br />
            a my skontaktujemy się z Tobą.
          </h2>
        </template>
        <template v-slot:content>
          <h4 class="error" v-if="sendingError">Wystąpił błąd podczas wysyłania, spróbuj ponownie później.</h4>
          <label>
            Imię (wymagane)
            <span
              class="error"
              v-if="$v.form.name.$error && !$v.form.name.required"
              >To pole jest wymagane</span
            >
            <span
              class="error"
              v-else-if="$v.form.name.$error && !$v.form.name.minLength"
              >Minimalna długość to 4 znaki</span
            >
            <input
              v-model="form.name"
              type="text"
              :class="[{ 'input--error': $v.form.name.$error }]"
            />
          </label>
          <label>
            Nazwisko (niewymagane)
            <input v-model="form.surname" type="text" /> </label
          ><label>
            Numer telefonu (wymagane)
            <span
              class="error"
              v-if="$v.form.phone.$error && !$v.form.phone.required"
              >To pole jest wymagane</span
            >
            <span
              class="error"
              v-else-if="$v.form.phone.$error && !$v.form.phone.phoneRegex"
              >Poprawny format numeru telefonu to 123-456-789, 123 456 789 lub 123456789.</span
            >
            <input
              v-model="form.phone"
              type="text"
              :class="[{ 'input--error': $v.form.phone.$error }]"
            /> </label
          ><label>
            Treść wiadomości (niewymagane)
            <textarea v-model="form.description" />
          </label>
          <label class="contact-form__agree">
            <input
              v-model="form.agree"
              type="checkbox"
              :class="[{ 'input--error': $v.form.agree.$error }]"
            />
            <span>
               <span
                 class="error"
                 v-if="$v.form.agree.$error && !$v.form.agree.checked"
               >Zgoda jest wymagana <br></span
               >
              Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do
              eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut
              enim ad minim veniam, quis nostrud exercitation ullamco laboris
              nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in
              reprehenderit in voluptate velit esse cillum dolore eu fugiat
              nulla pariatur. Excepteur sint occaecat cupidatat non proident,
              sunt in culpa qui officia deserunt mollit anim id est laborum.
            </span>
            <button :disabled="sending" type="submit">{{sending? 'WYSYŁANIE...':'WYŚLIJ'}}</button>
          </label>
        </template>
      </contact-form>
    </form>
  </div>
</template>

<script>
import Vue from "vue";
import Vuelidate from "vuelidate";
import { minLength, required } from "vuelidate/lib/validators";
import axios from "axios";
import ContactForm from "../../components/ContactForm";
Vue.use(Vuelidate);
const checked = value => value === true;
// eslint-disable-next-line no-useless-escape
const phoneRegex = value => /^[0-9\+]{8,13}$/.test(value.replace(/\s|-/g, ""));

export default {
  name: "CallMeView",
  components: { ContactForm },
  validations: {
    form: {
      name: {
        required,
        minLength: minLength(4)
      },
      phone: {
        required,
        phoneRegex
      },
      agree: {
        checked
      }
    }
  },
  props: {
    services: { type: Object }
  },
  data: function () {
    return {
      form: {
        name: "",
        surname: "",
        phone: "",
        agree: false
      },
      sending: false,
      sendingError: null
    };
  },
  methods: {
    async submit () {
      this.$v.$touch();
      if (!this.$v.$invalid) {
        this.sending = true;
        this.sendingError = null;
        try {
          await axios.post("/api/contact", { services: this.services, "contact-details": this.form });
          this.$emit("form-sent");
        } catch (e) {
          console.error(e);
          this.sendingError = e;
        } finally {
          this.sending = false;
        }
      }
    }
  }
};
</script>

<style lang="scss" scoped>
.contact-form {
  &--main-info-view {
    button {
      width: 100%;
      max-width: 218px;
      margin-right: 0;
    }
  }
}
</style>
