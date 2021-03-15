<template>
  <div class="contact-form--does-have-shop-view">
    <form class="form" @submit.prevent="submit">
      <contact-form>
        <template v-slot:header>
          <h2>
            <strong
              >Doskonale!<br />
              W jakiej technologii wykonano sklep?
            </strong>
          </h2>
          <div class="error" v-if="submitError && !shop">
            {{
              addressIsEmpty
                ? "Wpisz adress, aby przejść dalej"
                : anotherIsEmpty
                ? "Wpisz nazwę, aby przejść dalej"
                : "Zaznacz odpowiedź, aby przejść dalej"
            }}
          </div>
          <div class="great" v-else>
            {{
              isSelectedPrestaShop
                ? "Super!"
                : isSelectedWooCommerce
                ? "Super! Mamy doskonałą integrację z wtyczką WooCommerce."
                : isSelectedAnother && another.length
                ? "Hmmm… musimy sprawdzić ten sklep. Wrócimy do Ciebie z informacją."
                : isSelectedDontKnow
                ? "Nie szkodzi, nasi programiści ustalą to dla Ciebie. Podaj adres sklepu i wrócimy do Ciebie z informacją"
                : ""
            }}
          </div>
        </template>
        <template v-slot:content>
          <div class="radios">
            <label>
              <input
                name="shop"
                type="radio"
                value="WooCommerce"
                v-model="shop"
              /><span>WooCommerce</span>
            </label>
            <label>
              <input
                name="shop"
                type="radio"
                value="PrestaShop"
                v-model="shop"
              /><span>PrestaShop</span>
            </label>
            <label>
              <input
                name="shop"
                type="radio"
                value="dontKnow"
                v-model="shop"/><span
                >Nie wiem
                <input
                  v-if="isSelectedDontKnow"
                  type="text"
                  v-model="address"
                  class="input--address"
                  :class="[{ 'input--error': addressIsEmpty }]"/></span
            ></label>
            <label>
              <input
                name="shop"
                type="radio"
                value="another"
                v-model="shop"
              /><span
                >Inna
                <input
                  v-if="isSelectedAnother"
                  type="text"
                  class="input--another"
                  v-model="another"
                  :class="[{ 'input--error': anotherIsEmpty }]"
              /></span>
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
  name: "WhatTechnologyView",
  components: { ContactForm },
  props: {
    data: { type: Object }
  },
  data: function () {
    return {
      shop: "",
      another: "",
      anotherIsEmpty: false,
      address: "",
      addressIsEmpty: false,
      submitError: false
    };
  },
  computed: {
    isSelectedPrestaShop () {
      return this.shop === "PrestaShop";
    },
    isSelectedWooCommerce () {
      return this.shop === "WooCommerce";
    },
    isSelectedAnother () {
      return this.shop === "another";
    },
    isSelectedDontKnow () {
      return this.shop === "dontKnow";
    },
    technology () {
      if (this.isSelectedAnother) {
        return { shop: this.another };
      }
      if (this.isSelectedDontKnow) {
        return { shop: this.shop, address: this.address };
      }
      return { shop: this.shop };
    }
  },
  methods: {
    async submit () {
      this.anotherIsEmpty = false;
      this.addressIsEmpty = false;
      if (this.isSelectedAnother) {
        if (!this.another.length) {
          this.anotherIsEmpty = true;
          this.submitError = true;
          return;
        }
      }
      if (this.isSelectedDontKnow) {
        if (!this.address.length) {
          this.addressIsEmpty = true;
          this.submitError = true;
          return;
        }
      }
      if (!this.shop) {
        this.submitError = true;
        return;
      }
      this.$emit("next", this.technology);
    }
  },
  created () {
    if (this.data["shop-technology"] && this.data["shop-technology"].shop) {
      if (
        !["dontKnow", "PrestaShop", "WooCommerce"].includes(
          this.data["shop-technology"].shop
        )
      ) {
        this.shop = "another";
        this.another = this.data["shop-technology"].shop;
      } else {
        this.shop = this.data["shop-technology"].shop;
        if (this.data["shop-technology"].address) {
          this.address = this.data["shop-technology"].address;
        }
      }
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
  .great {
    height: 19px;
    text-align: center;
    color: #ff8730;
    margin-top: 35px;
  }
  .error {
    margin-bottom: 29px;
  }
  .radios {
    margin-top: 0;
    @media (max-width: 720px) {
      margin-top: 40px;
    }
    label {
      span {
        text-align: left;
        margin-left: 62px;
        width: calc(100% - 100px);
      }

      input[type="text"] {
        height: 30px;
        width: 127px;
        margin: 0 0 0 5px;
        &.input--address {
          width: 94px;
        }
      }
    }
  }
}
</style>
