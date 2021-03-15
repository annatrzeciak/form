<template>
  <div class="contact-form--main-info-view">
    <form class="form" @submit.prevent="submit">
      <contact-form>
        <template v-slot:header>
          <h2>
            <strong>Wypełnij ten formularz,</strong> dzięki czemu <br />
            <strong>przygotujemy rozwiązania</strong> na miarę Twoich potrzeb
          </h2>
        </template>
        <template v-slot:content>
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
            <input v-model="form.name" type="text"  />
          </label>
          <label>
            Nazwisko (niewymagane)
            <input v-model="form.surname" type="text" /> </label
          ><label>
            Email (wymagane)
          <span
            class="error"
            v-if="$v.form.email.$error && !$v.form.email.required"
          >To pole jest wymagane</span
          >
          <span
            class="error"
            v-else-if="$v.form.email.$error && !$v.form.email.email"
          >Wprowadzono niepoprawny format adresu email</span
          >
            <input v-model="form.email" type="email"  />
          </label>
          <label class="contact-form__agree">
            <input v-model="form.agree" type="checkbox"  />
            <span>
            Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do
            eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim
            ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut
            aliquip ex ea commodo consequat. Duis aute irure dolor in
            reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla
            pariatur. Excepteur sint occaecat cupidatat non proident, sunt in
            culpa qui officia deserunt mollit anim id est laborum.
              <span
                class="error"
                v-if="$v.form.agree.$error && !$v.form.agree.checked"
              ><br />Zgoda jest wymagana
              </span>
            </span>
          </label>
        </template>
        <template v-slot:footer>
          <button type="button" class="outline" @click="$emit('prev')">WSTECZ</button>
          <button type="submit">DALEJ</button>
        </template>
      </contact-form>
    </form>
  </div>
</template>

<script>
import Vuelidate from "vuelidate";
import { minLength, required, email } from "vuelidate/lib/validators";

import ContactForm from "../../components/ContactForm";
import Vue from "vue";
Vue.use(Vuelidate);
const checked = value => value === true;

export default {
  name: "MainInfoView",
  components: { ContactForm },
  validations: {
    form: {
      name: {
        required,
        minLength: minLength(4)
      },
      email: {
        required,
        email
      },
      agree: {
        checked
      }
    }
  },
  props: {
    data: { type: Object }
  },
  data: function () {
    return {
      form: {
        name: "",
        surname: "",
        email: "",
        agree: false
      }
    };
  },
  methods: {
    async submit () {
      this.$v.$touch();
      if (!this.$v.$invalid) {
        this.$emit("next", this.form);
      }
    }
  },
  created () {
    if (this.data["contact-details"]) {
      this.form.name = this.data["contact-details"].name;
      this.form.surname = this.data["contact-details"].surname;
      this.form.email = this.data["contact-details"].email;
      this.form.agree = this.data["contact-details"].agree;
    }
  }
};
</script>

<style lang="scss" scoped>
.contact-form {
}
</style>
