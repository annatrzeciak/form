<template>
  <main id="app">
    <contact />
  </main>
</template>

<script>
import Contact from './views/Contact'

export default {
  name: 'App',
  components: { Contact }
}
</script>

<style lang="scss">
@import url("https://fonts.googleapis.com/css2?family=Roboto:wght@300;400;700&display=swap");

body {
  margin: 0;
  padding: 0;
}

#app {
  font-family: Roboto;
}

input[type="checkbox"] {
  position: relative;

  &:before {
    box-sizing: border-box;
    height: 25px;
    width: 25px;
    content: "";
    border-radius: 50%;
    border: 1px solid #b4b4b4;
    display: block;
    background: #fff;
    position: absolute;
    left: calc(50% - 12px);
    top: calc(50% - 12px);
  }

  &:checked {
    &:before {
      border-color: #491989;
    }

    &:after {
      height: 15px;
      width: 15px;
      content: "";
      border-radius: 50%;
      display: block;
      background: #491989;
      position: absolute;
      left: calc(50% - 7px);
      top: calc(50% - 7px);
    }
  }
}

button {
  border-style: solid;
  height: 48px;
  border-radius: 3px;
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
}
</style>
