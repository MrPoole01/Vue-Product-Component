<template>
  <div id="app">
    <Nav/>
    <SockPage />
  </div>
</template>

<script>
import SockPage from '@/components/SockPage'
import Nav from '@/components/Nav'

export default {
  name: 'app',
  components: {
    SockPage,
    Nav
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
