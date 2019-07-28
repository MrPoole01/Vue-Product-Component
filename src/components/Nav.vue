<template>
  <div class="nav-bar">
    <div class="cart">Cart({{ cart.length }})</div>
  </div>
</template>

<script>
export default {
  props: [
    'inStock',
    'inventory',
    'variants',
    'selectedVariants',
    'cart',
    'addToCart'
  ],
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
  width: 100vw;
  position: fixed;
}

.cart {
  margin-right: 25px;
  margin-top: .5rem;
  float: right;
  border: 1px solid #d8d8d8;
  padding: 5px 20px;
}
</style>
