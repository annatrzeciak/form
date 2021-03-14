<template>
  <div class="contact-form">
    <div class="contact-form__header">
      <slot name="header"></slot>
    </div>
    <div class="contact-form__content">
      <slot name="content"></slot>
    </div>
    <div class="contact-form__footer">
      <slot name="footer"></slot>
    </div>
  </div>
</template>

<script>
export default {
  name: "ContactForm"
};
</script>

<style scoped lang="scss">
.contact-form {
  border: 1px solid #491989;
  border-radius: 5px;
  padding: 35px 57px;
  min-height: 704px;
  box-sizing: border-box;
  display: flex;
  flex-direction: column;
  @media (max-width: 968px) {
    margin-right: 20px;
    margin-left: 20px;
  }
  @media (max-width: 720px) {
    padding: 25px;
    min-height: auto;
  }

  h2 {
    margin-bottom: 0;
    font-size: 22px;
    font-weight: 300;
    text-align: center;
    color: #491989;
  }

  h3 {
    margin-top: 0;
    font-weight: 300;
    font-size: 22px;
    text-align: center;
    color: #491989;
  }

  @media (max-width: 720px) {
    h2,
    h3 {
      font-size: 18px;
    }
  }

  &__content {
    margin-top: 35px;

    .error {
      color: red;
      font-size: 12px;
      font-style: italic;
      @media (max-width: 720px) {
        display: inline-block;
        width: 100%;
      }
    }

    label {
      width: 100%;
      font-size: 15px;
      color: #000000;
      cursor: pointer;

      input[type="text"],
      input[type="email"],
      textarea {
        width: 100%;
        margin-top: 10px;
        margin-bottom: 22px;
        border-radius: 5px;
        border: 1px solid #b4b4b4;
        height: 48px;
        box-sizing: border-box;
        padding: 10px;
        font-size: 15px;

        &.input--error {
          border: 1px solid red;
        }

        &:focus {
          outline-color: #491989;
        }
      }

      textarea {
        height: 88px;
        font-family: Roboto;
      }

      input[type="checkbox"] {
        display: inline-block;
        width: 26px;
        height: 12px;

        &:before {
          border-radius: 5px;
          height: 22px;
          width: 22px;
        }

        &:checked:after {
          border-radius: 3px;
          height: 14px;
          width: 14px;
          left: calc(50% - 8px);
          top: calc(50% - 8px);
        }

        &.input--error:before {
          border-color: red;
        }
      }
    }

    label.contact-form__agree {
      box-sizing: border-box;
      padding-left: 5px;
      font-size: 12px;
      font-style: italic;
      color: #959595;
      line-height: 20px;
      display: flex;

      & > span {
        padding-left: 10px;
      }
    }

    .radios {
      display: flex;
      flex-direction: column;
      align-items: center;

      label {
        width: 265px;
        height: 48px;
        background: #f5f5f5;
        border-radius: 5px;
        font-size: 15px;
        margin-bottom: 20px;
        display: flex;
        align-items: center;
        padding-right: 18px;
        padding-left: 18px;
        box-sizing: border-box;
        position: relative;

        input[type="radio"] {
          &:before {
            height: 20px;
            width: 20px;
          }

          &:checked:after {
            height: 12px;
            width: 12px;

            left: calc(50% - 8px);
            top: calc(50% - 8px);
          }
        }
        span {
          width: calc(100% - 36px);
          position: absolute;
          text-align: center;
        }
      }
    }
  }

  &__footer {
    margin-top: auto;
    display: flex;
    justify-content: space-between;
    margin-bottom: 15px;
    @media (max-width: 560px) {
      flex-direction: column;
    }

    button {
      width: 214px;
      margin-right: 0;
      margin-left: 0;
      @media (max-width: 560px) {
        margin-top: 20px;
        margin-right: auto;
        margin-left: auto;
      }
    }
  }
}
</style>
