<template>
  <img alt="Vue logo" src="./assets/logo.png">
  <div id="app">
    <ContactHome />
  </div>
</template>

<script>
import ContactHome from './views/ContactHome.vue'

export default {
  name: 'App',
  components: {
    ContactHome
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
