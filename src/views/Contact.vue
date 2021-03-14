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
      <what-technology-view
        v-if="isVisibleWhatTechnology"
        :shop-technology="data['shop-technology']"
        @next="openNextView"
        @prev="openPrevView"
      /><does-have-shop-view
        v-else-if="isVisibleDoesHaveShop"
        :shop="data['has-shop']"
        @next="openNextView"
        @prev="openPrevView"
      />
      <main-info-view
        v-else-if="isVisibleMainInfo"
        :details="data['contact-details']"
        @next="openNextView"
        @prev="openPrevView"
      />
      <thank-you-view v-else-if="isVisibleThankYou" />
      <call-me-view
        v-else-if="isVisibleCallMeForm"
        :services="services"
        :details="data['contact-details']"
        @form-sent="formSent"
      />
      <main-contact-view
        v-else
        :printilo="services"
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

export default {
  name: "Contact",
  components: {
    WhatTechnologyView,
    DoesHaveShopView,
    MainInfoView,
    ThankYouView,
    CallMeView,
    MainContactView
  },
  data: function () {
    return {
      isVisibleWhatTechnology: false,
      isVisibleDoesHaveShop: false,
      isVisibleThankYou: false,
      isVisibleCallMeForm: false,
      isVisibleMainInfo: false,
      services: {},
      data: {}
    };
  },
  methods: {
    openNextView (data) {
      if (this.isVisibleMainInfo) {
        this.data["contact-details"] = data;
        this.isVisibleDoesHaveShop = true;
        this.isVisibleMainInfo = false;
      } else if (this.isVisibleDoesHaveShop) {
        this.data["has-shop"] = data;
        if (this.data["has-shop"]) {
          this.isVisibleWhatTechnology = true;
        }
        this.isVisibleDoesHaveShop = false;
      } else if (this.isVisibleWhatTechnology) {
        this.data["shop-technology"] = data;
        this.isVisibleWhatTechnology = false;
      }
    },
    openPrevView () {
      if (this.isVisibleMainInfo) {
        this.isVisibleMainInfo = false;
      } else if (this.isVisibleDoesHaveShop) {
        this.isVisibleMainInfo = true;
        this.isVisibleDoesHaveShop = false;
      } else if (this.isVisibleWhatTechnology) {
        this.isVisibleWhatTechnology = false;
        this.isVisibleDoesHaveShop = true;
      }
    },
    showDescribeForm (services) {
      this.services = services;
      this.isVisibleMainInfo = true;
    },
    showCallMeForm (services) {
      this.services = services;
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
