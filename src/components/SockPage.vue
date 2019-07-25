<template>
    <div class="product">
      <div class="product-image">
        <img :src="image" />
      </div>

      <div class="product-info">
        <h1>
          <a :href="image">{{ title }}</a>
          <br><span v-if="onSale"> On Sale</span>
        </h1>

        <p v-if="inStock > 10">InStock</p>
        <p v-else-if="inStock <= 10 && inStock > 0">
          Almost gone... only {{ inventory }} remaining!</p>
        <p v-else class="os">Out of Stock</p>

        <p>
          {{ description }}
        </p>

          <ul>
            <li v-for="detail in details" :key="detail.id">{{ detail }}</li>
          </ul>

        <select v-model="size">
          <option :value="size" disabled>select a size</option>
          <option v-for="size in sizes" :key="size.sizeID">
            {{ size.sizeFit }}
          </option>
        </select>

        <div class="box-container">
          <div  class="color-box" 
                v-for="(variant, index) in variants" 
                :key="variant.variantId"
                :style="{ backgroundColor: variant.variantColor }"
                @mouseover="updateProduct(index)"
                >
          </div>
        </div>

        <div class="button-container">
          <button @click="addToCart"
                  :disabled="!inStock"
                  :class="{ disabledButton: !inStock }"> 
                  Add to Cart
          </button>
          <button @click="removeFromCart"
                  class="remove-button"> 
                  Remove from Cart
          </button>
        </div>

      </div>
    </div>
</template>

<script>

export default {
  name: 'socks',
  props: [
    'name',
    'brand',
    'description',
    'selectedVariant',
    'onSale',
    'details',
    'variants',
    'size',
    'sizes',
    'updateProduct',
    'title',
    'image',
    'inStock',
    'inventory',
  ],
  data() {
    return {
      
    };
  },
  methods: {

    addToCart() {
      this.$emit('add-to-cart', this.variants[this.selectedVariant].variantId)
    },
    removeFromCart() {
      this.$emit('remove-from-cart', this.variants[this.selectedVariant].variantId)
    }
  },
  vue: {
    loaders: {
      scss: "style!css!sass"
    }
  },
  
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
body {
  font-family: tahoma;
  color: #282828;
  margin: 0px;
}

.product {
  display: flex;
  margin-left: -3rem;

  p {
    font-weight: bold;
  }

  p.os {
      text-decoration: line-through;
    }

  span {
    font-size: 16px;
    color: red;
  }

  span.selected {
    color: black;
  }

  a {
    text-decoration: none;
    color: black;
  }
}

img {
  border: 1px solid #d8d8d8;
  width: 70%;
  margin: 40px;
  box-shadow: 0px 0.5px 1px #d8d8d8;
}

.product-image {
  flex-basis: 700px;
  margin: 0;
}

.product-info {
  margin-top: 10px;
  text-align: left;
  flex-basis: 500px;
}

.box-container {
  display: flex;
  flex-direction: row;
}

.color-box {
  width: 40px;
  height: 40px;
  margin: 1rem .3rem;
}

.button-container {
  display: flex;
}

button {
  margin: 30px .3rem;
  border: none;
  background-color: #1e95ea;
  color: white;
  height: 40px;
  width: 100px;
  font-size: 14px;
}

.disabledButton {
  background-color: #d8d8d8;
}

.remove-button {
  background-color: #c41212;
}

.review-form {
  width: 30%;
  padding: 20px;
  border: 1px solid #d8d8d8;
}

input {
  width: 100%;
  height: 25px;
  margin-bottom: 20px;
}

textarea {
  width: 100%;
  height: 60px;
}
</style>
