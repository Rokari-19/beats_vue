<template>

  <div class="home">
    <section class="hero box is-medium mb-6 is-dark is-rounded modi">
      
      <!-- <figure class="is-justify-content-left is-32x32 ">
        <img src="../assets/silver-02-solo3.jpg.large.2x.jpg">
      </figure> -->

      <div class="hero-body has-text-centered">
        <p class="title mb-6 has-text-base">
          beats.com
        </p>
        <p class="subtitle has-text-base">
          The Place for everything Beats
        </p>
      </div>
    </section>

    <div class="columns is-multiline">

      <div class="column is-12">

        <h2 class="is-size-2 has-text-centered has-text-dark">
          New In Stock
        </h2>

      </div>
      
      <ProductBox v-for="product in latestProducts" v-bind:key="product.id" v-bind:product="product"/>

    </div>
    <section class="hero  my-auto ">
      <div class="columns is-multiline my-6">
        
        <div class="column is-12">
        
          <h1 class="title is-size-4 has-text-centered has-text-dark my-6">
            Seamless payments powered by Stripe&#174;
          </h1>

        </div>

        <div class="column is-4">
          <h2 class="subtitle has-text-centered has-text-dark has-text-weight-semibold mx-auto">
            In-Store pickup
          </h2>
          <p class="has-text-dark">
            Pick up your online order at a Trusted Retailer near you.
          </p>
          <div class="">
            <a href="#" class="has-text-link">Find a Retailer Near you</a>
          </div>
        </div>

        <div class="column is-4">
          <h2 class="subtitle has-text-centered has-text-dark has-text-weight-semibold mx-auto">
            Nation-Wide Delivery options
          </h2>
          <p class="has-text-dark">
            Affordable shipping from our office to anywhere in Nigeria
          </p>
          <div class="">
            <a href="/stores" class="has-text-link">Learn More</a>
          </div>
        </div>

        <div class="column is-4">
          <h2 class="subtitle has-text-centered has-text-dark has-text-weight-semibold mx-auto">
            Easy Returns
          </h2>
          <p class="has-text-dark">
            Something wrong with your order? Return eligible items to us within 14 days of purchase.
          </p>
          <div class="">
            <a href="#" class="has-text-link">Try it out</a>
          </div>
        </div>
      </div>
    </section>

  </div>
</template>
<style>
.modi {
  background: url(../assets/safarulla-kasmi-uTPkovVRhR8-unsplash.jpg);
  
}
.pic {
    border-radius: 1px;
}

.op {
  opacity: 1;
}
</style>

<script>
// @ is an alias to /src
import axios from 'axios'
import ProductBox from '@/components/ProductBox.vue'

export default {
  name: 'HomeView',
  
  data () {
    return {
      latestProducts: []
    };
  },
  
  components: {
    ProductBox
  },
  
  mounted () {
    this.getLatestProducts()

    document.title = 'Home | beats.com'
  },

  methods: {
    async getLatestProducts() {
      this.$store.commit('setIsLoading', true)

      await axios
          .get('/api/v1/latest-products/')
          .then(response => {
            this.latestProducts = response.data
          })
          .catch(error => {
            console.log(error)
          })

      this.$store.commit('setIsLoading', false)

    }
  }
}
</script>



