<template>
  <div class="container">

    <span class="tabs" 
      :class="{ activeTab: selectedTab === tab}"
      v-for="(tab, index) in tabs"
      :key="index"
      @click="selectedTab = tab"
      >{{ tab }}
    </span>

    <div class="reviews" v-show="selectedTab === 'Reviews'">
      <h2>Reviews</h2>
      <p v-if="!reviews.length">There are no reviews yet.</p>
      <ul>
        <li v-for="review in reviews" :key="review">
        <p>{{ review.name }} <br> Rating: {{ review.rating }}</p>
        <p>{{ review.review }}</p>
        </li>
      </ul>
    </div>

    <hr>

    <form 
      class="review-form" 
      @submit.prevent="onSubmit"
      v-show="selectedTab === 'Make A Review' "
      >
      
        <p class="error" v-if="errors.length">
          <b>Please correct the following error(s):</b>
          <ul>
            <li v-for="error in errors" :key="error">{{ error }}</li>
          </ul>
        </p>

        <p>
          <label for="name">Name:</label>
          <input id="name" v-model="name">
        </p>
        
        <p>
          <label for="review">Review:</label>      
          <textarea id="review" v-model="review"></textarea>
        </p>
        
        <p>
          <label for="rating">Rating:</label>
          <select id="rating" v-model.number="rating">
            <option>5</option>
            <option>4</option>
            <option>3</option>
            <option>2</option>
            <option>1</option>
          </select>
        </p>

        <p>Would you recommend this product?</p>
          <label>
            Yes
          <input type="radio" value="Yes" v-model="recommend"/>
          </label>
          <label>
            No
          <input type="radio" value="No" v-model="recommend"/>
          </label>
        <p>
          <input type="submit" value="Submit">  
        </p>    
      
    </form>
  </div>
</template>

<script>
export default {
  props: {
      reviews: {
      type: Array,
      required: true
    },
      addReviews: {
      type: Array,
      required: true
      }
  },
  data() {
    return {
      tabs: ['Reviews', 'Make A Review'],
      selectedTab: 'Reviews',
      name: null,
      review: null,
      rating: null,
      recommend: null,
      index: [],
      errors: []
    }
  },
  methods: {
    onSubmit() {
      this.errors = []
      if(this.name && this.review && this.rating && this.recommend) {
        let productReview = {
          name: this.name,
          review: this.review,
          rating: this.rating,
          recommend: this.recommend
        }        
        this.$emit('review-submitted', productReview)
        this.name = null
        this.review = null
        this.rating = null
        this.recommend = null
      } else {
        if(!this.name) this.errors.push("Name required.")
        if(!this.review) this.errors.push("Review required.")
        if(!this.rating) this.errors.push("Rating required.")
        if(!this.recommend) this.errors.push("Recommendation required.")
      }
    }
  }
}
</script>

<style scoped lang="scss">

.container {
  display: block;
  flex-direction: row;
  justify-content: left;
  margin: 3.5%;

  .reviews {
    text-align: left;
  }

  .review-form {
    display: inline-block;
    max-width: 50%;
    padding: 20px;
    border: 1px solid #d8d8d8;
  }

  input {
    width: 100%;
    height: 25px;
    margin-bottom: -.2rem;
  }

  textarea {
    width: 100%;
    height: 100px;
  }

  .tabs {
    margin-left: 20px;
    cursor: pointer;
  }

  hr {
    margin: 1.3rem;
  }

  .activeTab {
    color: #16C0B0;
    text-decoration: underline;
    font-size: 20px;
  }

}

</style>

