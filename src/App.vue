<template>
  <div id="app">
    <SockPage />
  </div>
</template>

<script>
import SockPage from './components/SockPage.vue'

export default {
  name: 'app',
  components: {
    SockPage
  }
}
</script>

<style lang="scss">
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
