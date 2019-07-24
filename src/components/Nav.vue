<template>
  <div class="nav-bar"></div>
</template>

<script>
export default {
  data() {
    return {
      
    }
  },
  vue: {
    loaders: {
      scss: "style!css!sass"
    }
  }
}
</script>

<style scoped lang="scss">

.nav-bar {
  background: linear-gradient(-90deg, #84cf6a, #16c0b0);
  height: 60px;
  margin-bottom: 15px;
  margin-top: -3.8rem;
}

</style>
