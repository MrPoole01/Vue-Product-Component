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

        <ul>
          <li v-for="detail in details" :key="detail.id">{{ detail }}</li>
        </ul>

        <select v-model="size">
          <option :value="size" disabled>select a size</option>
          <option v-for="size in sizes" :key="size.sizeID">
            {{ size.sizeFit }}
          </option>
        </select>

        <div  class="color-box" 
              v-for="(variant, index) in variants" 
              :key="variant.variantId"
              :style="{ backgroundColor: variant.variantColor }"
              @mouseover="updateProduct(index)"
              >
        </div>

        <button @click="addToCart"
                :disabled="!inStock"
                :class="{ disabledButton: !inStock }"> 
                Add to Cart
        </button>

        <div class="cart">
          Cart({{ cart }})
        </div>
      </div>
    </div>
</template>

<script>

export default {
  name: 'socks',
  data() {
    return {
      name: "SockPage",
      brand: "SuperVue",
      product: "Socks",
      selectedVariant: 0,
      onSale: true,
      details: ["80% Cotton", "20% Polyester", "Gender Neutral"],
      variants: [
        {
          variantId: "2234",
          variantColor: "green",
          variantImage: "./assets/vmSocks-green-onWhite.jpg",
          variantQuantity: 10
        },
        {
          variantId: "2235",
          variantColor: "blue",
          variantImage: "./assets/vmSocks-blue-onWhite.jpg",
          variantQuantity: 0
        }
      ],
      size: "",
      sizes: [
        {
          sizeID: "1234",
          sizeFit: "small"
        },
        {
          sizeID: "1235",
          sizeFit: "medium"
        },
        {
          sizeID: "1236",
          sizeFit: "large"
        },
        {
          sizeID: "1237",
          sizeFit: "X large"
        }
      ],
      cart: 0
    };
  },
  vue: {
    loaders: {
      scss: "style!css!sass"
    }
  },
  methods: {

    addToCart() {
      this.cart += 1
      this.variants[this.selectedVariant].variantQuantity -= 1
    },
    updateProduct(index) {
      this.selectedVariant = index      
    }
  },
  computed: {
    title() {
      return this.brand + ' ' + this.product 
    },
    image() {
      return this.variants[this.selectedVariant].variantImage
    },
    inStock() {
      return this.variants[this.selectedVariant].variantQuantity
    },
    inventory() {
      return this.variants[this.selectedVariant].variantQuantity
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

.color-box {
  width: 40px;
  height: 40px;
  margin-top: 1rem;
}

.cart {
  margin-right: 25px;
  margin-top: 2rem;
  float: right;
  border: 1px solid #d8d8d8;
  padding: 5px 20px;
}

button {
  margin-top: 30px;
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
