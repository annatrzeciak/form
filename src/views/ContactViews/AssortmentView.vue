<template>
  <div class="contact-form--assortment-view">
    <form class="form" @submit.prevent="submit">
      <contact-form>
        <template v-slot:header>
          <h2>
            <strong v-if="data['has-shop']"
              >Chcielibyśmy wiedzieć jakie produkty
              <br />
              masz zamiar personalizować w swoim sklepie.
            </strong>
            <strong v-else
              >Czyli myślisz o założeniu sklepu? <br />Doskonale trafiłeś!<br />To
              nasza specjalność. Skontaktujemy się z Tobą najszybciej jak to
              możliwe.
              <br />
              Powiedz nam jeszcze jaki asortyment Cię interesuje.
            </strong>
          </h2>
          <div class="error">
            {{
              submitError && !selectedAssortment.length
                ? "Zaznacz odpowiedź, aby przejść dalej"
                : ""
            }}
          </div>
        </template>
        <template v-slot:content>
          <div class="checkboxes">
            <label v-for="item in assortment" :key="item.key">
              <input type="checkbox" v-model="item.value" /><span
                v-html="item.label"
              ></span>
            </label>
          </div>
        </template>
        <template v-slot:footer>
          <button type="button" class="outline" @click="$emit('prev')">
            WSTECZ
          </button>
          <button type="submit">DALEJ</button>
        </template>
      </contact-form>
    </form>
  </div>
</template>

<script>
import ContactForm from "../../components/ContactForm";

export default {
  name: "AssortmentView",
  components: { ContactForm },
  props: {
    data: { type: Object }
  },
  data: function () {
    return {
      assortment: [
        {
          value: false,
          key: "clothes",
          label: "odzież"
        },
        {
          value: false,
          key: "animalAccessories",
          label: "akcesoria dla zwierząt"
        },
        {
          value: false,
          key: "shoes",
          label: "obuwie"
        },
        {
          value: false,
          key: "toys",
          label: "zabawki"
        },
        {
          value: false,
          key: "accessories",
          label: "galanteria i dodatki"
        },
        {
          value: false,
          key: "sportAccessories",
          label: "akcesoria<br>sportowe/hobbistyczne"
        },
        {
          value: false,
          key: "jewelry",
          label: "biżuteria"
        },
        {
          value: false,
          key: "carAccessories",
          label: "akcesoria<br>sportowe/hobbistyczne"
        },
        {
          value: false,
          key: "homeAndGardenEquipment",
          label: "wyposażenie wnętrz<br>i ogrodów"
        },
        {
          value: false,
          key: "printingProducts",
          label: "produkty poligraficzne"
        }
      ],

      submitError: false
    };
  },
  computed: {
    selectedAssortment () {
      return this.assortment.filter(item => item.value);
    }
  },
  methods: {
    async submit () {
      if (!this.selectedAssortment || !this.selectedAssortment.length) {
        this.submitError = true;
        return;
      }
      this.$emit(
        "next",
        this.selectedAssortment.map(item => ({
          key: item.key,
          label: item.label
        }))
      );
    }
  },
  created () {
    if (this.data["shop-assortment"] && this.data["shop-assortment"].length) {
      this.assortment.map(
        item =>
          (item.value = Boolean(
            this.data["shop-assortment"].find(as => as.key === item.key)
          ))
      );
    }
  }
};
</script>

<style lang="scss" scoped>
.contact-form {
  @media (max-width: 651px) {
    padding-right: 0;
    padding-left: 0;
  }
  &--assortment-view {
    h2 {
      margin-top: 60px;
      @media (max-width: 720px) {
        margin-top: 30px;
      }
    }

    .checkboxes {
      flex-direction: row;
      flex-wrap: wrap;
      max-width: 560px;
      margin-right: auto;
      margin-left: auto;
      @media (max-width: 651px) {
        flex-direction: column;
      }

      label {
        margin-right: 7.5px;
        margin-left: 7.5px;
        @media (max-width: 651px) {
          margin-right: auto;
          margin-left: auto;
        }

        span {
          text-align: left;
          position: relative;
          margin-left: 20px;
        }
      }
    }
  }
}
</style>
