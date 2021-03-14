<template>
  <div class="contact-form--does-have-shop-view">
    <form class="form" @submit.prevent="submit">
      <contact-form>
        <template v-slot:header>
          <h2>
            <strong
              >Czy posiadasz<br />
              sklep internetowy?</strong
            >
          </h2>
        </template>
        <template v-slot:content>
          <div class="radios">
            <label>
              <input
                name="shop"
                type="radio"
                :value="true"
                v-model="hasShop"
              /><span>TAK</span>
            </label>
            <label>
              <input
                name="shop"
                type="radio"
                :value="false"
                v-model="hasShop"
              /><span>NIE</span>
            </label>
          </div>
        </template>
        <template v-slot:footer>
          <button type="button" class="outline" @click="$emit('prev')">
            WSTECZ
          </button>
          <button type="submit">DALEJ</button></template
        >
      </contact-form>
    </form>
  </div>
</template>

<script>
import ContactForm from "../../components/ContactForm";

export default {
  name: "DoesHaveShopView",
  components: { ContactForm },
  props: {
    shop: { type: Boolean }
  },
  data: function () {
    return {
      hasShop: true
    };
  },
  methods: {
    async submit () {
      this.$emit("next", this.hasShop);
    }
  },
  created () {
    if (this.shop !== undefined) {
      this.hasShop = this.shop;
    }
  }
};
</script>

<style lang="scss" scoped>
.contact-form {
  h2 {
    margin-top: 60px;
    @media (max-width: 720px) {
      margin-top: 30px;
    }
  }
  .radios {
    margin-top: 85px;
    @media (max-width: 720px) {
      margin-top: 40px;
    }
    label{
      font-weight: bold;
    }
  }
}
</style>
