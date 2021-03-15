<template>
  <div class="contact-page">
    <header>
      <div>
        <h1>
          <strong>szukam</strong><br />
          kreatora
        </h1>
      </div>
      <div>
        <img src="/iPad.png" alt="IPad - aplikacja" title="Kreator - IPad" />
      </div>
    </header>
    <section class="contact-form-section">
      <assortment-view
        v-if="isVisibleAssortment"
        :data="data"
        @next="openNextView"
        @prev="openPrevView"
      />
      <what-technology-view
        v-else-if="isVisibleWhatTechnology"
        :data="data"
        @next="openNextView"
        @prev="openPrevView"
      /><does-have-shop-view
        v-else-if="isVisibleDoesHaveShop"
        :data="data"
        @next="openNextView"
        @prev="openPrevView"
      />
      <main-info-view
        v-else-if="isVisibleMainInfo"
        :data="data"
        @next="openNextView"
        @prev="openPrevView"
      />
      <thank-you-view v-else-if="isVisibleThankYou" />
      <call-me-view
        v-else-if="isVisibleCallMeForm"
        :data="data"
        @form-sent="formSent"
      />
      <main-contact-view
        v-else
        :data="data"
        @start-describe="showDescribeForm"
        @show-call-me-form="showCallMeForm"
      />
    </section>
  </div>
</template>

<script>
import MainContactView from "./ContactViews/MainContactView";
import CallMeView from "./ContactViews/CallMeView";
import ThankYouView from "./ContactViews/ThankYouView";
import MainInfoView from "./ContactViews/MainInfoView";
import DoesHaveShopView from "./ContactViews/DoesHaveShopView";
import WhatTechnologyView from "./ContactViews/WhatTechnologyView";
import AssortmentView from "./ContactViews/AssortmentView";

export default {
  name: "Contact",
  components: {
    AssortmentView,
    WhatTechnologyView,
    DoesHaveShopView,
    MainInfoView,
    ThankYouView,
    CallMeView,
    MainContactView
  },
  data: function () {
    return {
      step: 0,
      isVisibleThankYou: false,
      isVisibleCallMeForm: false,
      data: {}
    };
  },
  computed: {
    isVisibleMainInfo () {
      return this.step === 1;
    },
    isVisibleDoesHaveShop () {
      return this.step === 2;
    },
    isVisibleWhatTechnology () {
      return this.step === 3;
    },
    isVisibleAssortment () {
      return this.step === 4;
    },
    isVisibleMoreDetails () {
      return this.step === 5;
    },
    isVisibleThankForFinishedForm () {
      return this.step === 5;
    }
  },
  methods: {
    openNextView (data) {
      if (this.isVisibleMainInfo) {
        this.data["contact-details"] = data;
      } else if (this.isVisibleDoesHaveShop) {
        this.data["has-shop"] = data;
        if (!this.data["has-shop"]) {
          this.step++;
        }
      } else if (this.isVisibleWhatTechnology) {
        this.data["shop-technology"] = data;
      } else if (this.isVisibleAssortment) {
        this.data["shop-assortment"] = data;
      }
      this.step++;
    },
    openPrevView () {
      if (this.isVisibleMainInfo) {
        this.data["contact-details"] = null;
      } else if (this.isVisibleDoesHaveShop) {
        this.data["has-shop"] = null;
      } else if (this.isVisibleWhatTechnology) {
        this.data["shop-technology"] = null;
      } else if (this.isVisibleAssortment) {
        this.data["shop-assortment"] = null;
        this.isVisibleAssortment = false;
        if (!this.data["has-shop"]) {
          this.step--;
        }
        this.step--;
      }
    },
    showDescribeForm (services) {
      this.data.services = services;
      this.step++;
    },
    showCallMeForm (services) {
      this.data.services = services;
      this.isVisibleCallMeForm = true;
    },
    formSent () {
      this.isVisibleThankYou = true;
      this.isVisibleCallMeForm = false;
    }
  }
};
</script>

<style lang="scss" scoped>
.contact-page {
  header {
    max-width: 100%;
    width: calc(100vw - (100vw - 968px) / 2);
    margin-left: auto;
    margin-right: 0;
    display: flex;
    position: relative;
    @media (max-width: 678px) {
      flex-direction: column;
    }

    div {
      float: left;
      height: 462px;
      box-sizing: border-box;
      width: 50%;

      @media (max-width: 968px) {
        height: auto;
      }
      @media (max-width: 678px) {
        width: 100%;
      }

      &:first-of-type {
        padding-left: 58px;
        padding-top: 50px;
        background-image: url("/top_bg2.jpeg");
        background-size: cover;
        background-position: center right;
        display: flex;
        align-items: flex-end;
        @media (max-width: 678px) {
          padding-left: 25px;
        }
      }

      &:nth-of-type(2) {
        padding-top: 50px;
        background-image: url("/top_bg1.jpeg");
        background-size: cover;
        background-position: center left;
        @media (max-width: 1100px) {
          display: flex;
          justify-content: center;
        }

        img {
          position: absolute;
          left: calc(50% - 210px);
          bottom: 50px;
          @media (max-width: 1100px) {
            position: static;
            margin-bottom: 50px;
            max-width: 90%;
          }
        }
      }

      h1 {
        font-size: 65px;
        font-weight: normal;
        color: #fff;
        @media (max-width: 678px) {
          font-size: 50px;
        }
      }
    }
  }

  .contact-form-section {
    margin: 130px auto;
    max-width: 968px;
    width: 100%;
  }
}
</style>
