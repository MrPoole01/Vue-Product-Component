<template>
  <div class="container">

    <!-- <div>
      <span class="tab" 
        v-for="(tab, index) in tabs"
        :key="tab"
        @click="selectedTab = tab"
        >{{ tab }}
      </span>
    </div> -->

    <div>
        <h2>Reviews</h2>
        <p v-if="!reviews.length">There are no reviews yet.</p>
        <ul>
          <li v-for="review in reviews" :key="review">
          <p>{{ review.name }}</p>
          <p>Rating: {{ review.rating }}</p>
          <p>{{ review.review }}</p>
          </li>
        </ul>
    </div>

    <form class="review-form" @submit.prevent="onSubmit">
      
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
  data() {
      return {
        name: null,
        index: "",
        reviews:[],
        review: null,
        rating: null,
        recommend: null,
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
    },
     addReview(productReview) {
      this.reviews.push(productReview)
    }
  }
}
</script>

<style scoped lang="scss">

.container {
  display: flex;
  flex-direction: column;
  justify-content: left;
  margin: 4%;
}

.review-form {
  max-width: 100vw;
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
  height: 60px;
}
</style>

