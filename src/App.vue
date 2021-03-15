<template>
  <main id="app">
    <contact />
  </main>
</template>

<script>
import Contact from "./views/Contact";

export default {
  name: "App",
  components: { Contact }
};
</script>

<style lang="scss">
@import url("https://fonts.googleapis.com/css2?family=Roboto:ital,wght@0,300;0,400;0,700;1,300&display=swap");

body {
  margin: 0;
  padding: 0;
}

#app {
  font-family: Roboto;
}

input[type="checkbox"], input[type="radio"]{
  position: relative;

  &:before {
    box-sizing: border-box;
    height: 25px;
    width: 25px;
    content: "";
    border: 1px solid #b4b4b4;
    display: block;
    background: #fff;
    position: absolute;
    border-radius: 50%;
    left: calc(50% - 12px);
    top: calc(50% - 12px);
  }
  &:focus:before{
    border-color: #491989;
  }

  &:checked {
    &:before {
      border-color: #491989;
    }

    &:after {
      height: 15px;
      width: 15px;
      content: "";
      display: block;
      background: #491989;
      position: absolute;
      border-radius: 50%;
      left: calc(50% - 7px);
      top: calc(50% - 7px);
    }
  }
}

button {
  border-style: solid;
  height: 48px;
  border-radius: 5px;
  box-sizing: border-box;
  font-size: 15px;
  color: #fff;
  font-weight: bold;
  margin-right: 25px;
  margin-left: 25px;
  transition: 0.3s;
  cursor: pointer;
  border-color: #491989;
  background: #491989;

  &:active {
    transform: scale(0.9);
  }

  &:hover {
    background: #fff;
    color: #491989;
  }
  &:focus{
    outline-color: #491989;
  }
  &.outline {
    background: #fff;
    color: #491989;
    &:hover {
      background: #491989;
      color: #fff;
    }
  }
}
</style>
