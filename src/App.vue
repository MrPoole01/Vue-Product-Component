<template>
  <div id="app">
    <Nav
      :inStock="inStock"
      :inventory="inventory"
      :variants="variants"
      :selectedVariant="selectedVariant"
      :cart="cart"
    />
    <SockPage
      :name="name"
      :brand="brand"
      :description="description"
      :variants="variants"
      :selectedVariant="selectedVariant"
      :onSale="onSale"
      :details="details"
      :size="size"
      :sizes="sizes"
      :updateProduct="updateProduct"
      :title="title"
      :image="image"
      :inStock="inStock"
      :inventory="inventory"
      @add-to-cart="updateCart"
      @remove-from-cart="removeItem"
    />

    <ProductReviews 
      :reviews="reviews"
      @review-submitted="addReview"
    />
  </div>
</template>

<script>
import SockPage from "@/components/SockPage";
import Nav from "@/components/Nav";
import ProductReviews from "@/components/ProductReviews";
//import { log } from 'util';

export default {
  name: "app",
  components: {
    ProductReviews,
    SockPage,
    Nav
  },
  data() {
    return {
      name: "SockPage",
      brand: "SuperVue",
      product: "Socks",
      description:
        "Socks are the #1 most requested clothing item in homeless shelters, so we donate 1 pair of socks for every pair purchased. From the beginning, the Bombas mission has been to contribute to the homeless community and encourage others to get involved.",
      selectedVariant: 0,
      onSale: true,
      cart: [],
      details: ["80% Cotton", "20% Polyester", "Gender Neutral"],
      variants: [
        {
          variantId: "2234",
          variantColor: "green",
          variantImage: "./assets/vmSocks-green-onWhite.jpg",
          variantQuantity: 20
        },
        {
          variantId: "2235",
          variantColor: "blue",
          variantImage: "./assets/vmSocks-blue-onWhite.jpg",
          variantQuantity: 5
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
      reviews: []
    };
  },
  methods: {
    updateCart(id) {
      this.cart.push(id);
      this.variants[this.selectedVariant].variantQuantity -= 1;
    },
    removeItem(id) {
      for (var i = this.cart.length - 1; i >= 0; i--) {
        if (this.cart[i] === id) {
          this.cart.splice(i, 1);
        }
      }
    },
    updateProduct(index) {
      this.selectedVariant = index;
    },
    addReview(productReview) {
    this.reviews.push(productReview)
    }
  },
  computed: {
    title() {
      return this.brand + " " + this.product;
    },
    image() {
      return this.variants[this.selectedVariant].variantImage;
    },
    inStock() {
      return this.variants[this.selectedVariant].variantQuantity;
    },
    inventory() {
      return this.variants[this.selectedVariant].variantQuantity;
    }
  }
};
</script>

<style lang="scss">
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
