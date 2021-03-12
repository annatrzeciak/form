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
@import url('https://fonts.googleapis.com/css2?family=Roboto:wght@400;700&display=swap');
body{
  margin: 0;
  padding: 0;
}
#app {
  font-family: Roboto;
}
</style>
