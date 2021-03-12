<template>
  <div class="contact-form--main-view">
    <h2>Które rozwiązanie Cię interesuje?</h2>
    <h3>Wybierz jedno lub więcej z poniższych</h3>
    <div class="options">
      <label>
        <img src="/create.png" alt="" />
        <span> PRINTILO <strong>CREATE</strong> </span>
        <input type="checkbox" v-model="printiloCreate" />
      </label>
      <label>
        <img src="/photo.png" alt="" />
        <span> PRINTILO <strong>PHOTO</strong> </span>
        <input type="checkbox" v-model="printiloPhoto" />
      </label>
      <label>
        <img src="/clothes.png" alt="" />
        <span> PRINTILO <strong>CLOTHES</strong> </span>
        <input type="checkbox" v-model="printiloClothes" />
      </label>
    </div>
    <div class="buttons">
      <button @click="$emit('show-call-form', printlo)" class="call">
        Zadzwońcie do mnie
      </button>
      <span>lub</span>
      <button @click="$emit('start-describe', printlo)" class="start-form">
        Opiszę czego potrzebuję
      </button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'MainContactView',
  data: function () {
    return {
      services: {
        printiloCreate: false,
        printiloPhoto: false,
        printiloClothes: false
      }
    }
  },
  computed: {
    printlo: function () {
      return {
        printiloCreate: this.printiloCreate,
        printiloPhoto: this.printiloPhoto,
        printiloClothes: this.printiloClothes
      }
    }
  }
}
</script>

<style lang="scss" scoped>
.contact-form--main-view {
  .options {
    margin-top: 90px;
    display: flex;
    justify-content: center;
    @media (max-width: 720px) {
      flex-direction: column;
      margin-top: 30px;
    }
    label {
      display: flex;
      flex-direction: column;
      align-items: center;
      transition: 0.3s;
      cursor: pointer;
      img {
        margin-left: 64px;
        margin-right: 64px;
        margin-bottom: 50px;
        transition: 0.3s;
        max-width: 100%;
        @media (max-width: 720px) {
          margin-bottom: 20px;
        }
      }

      span {
        margin-bottom: 37px;
        @media (max-width: 720px) {
          margin-bottom: 10px;
        }
      }
      input {
        @media (max-width: 720px) {
          margin-bottom: 40px;
        }
      }

      &:hover {
        img {
          opacity: 0.8;
        }
      }

      &:active {
        transform: scale(0.9);
      }
    }
  }

  .buttons {
    margin-top: 82px;
    text-align: center;
    @media (max-width: 720px) {
      margin-top: 30px;
      span {
        display: block;
        margin-bottom: 15px;
      }
    }
    button {
      width: 214px;
      @media (max-width: 720px) {
        margin-bottom: 15px;
        margin-right: auto;
        margin-left: auto;
      }
      &.call {
        border-color: #ff8730;
        background: #ff8730;
        &:hover {
          background: #fff;
          color: #ff8730;
        }
      }
    }
  }
}
</style>
