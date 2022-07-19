<template>
  <div class="home">
    <div class="splash-container">
      <div class="splash">
        <h1>Splendid Food</h1>
      </div>
    </div>

    <main class="wrapper">
      <h2>Recommended</h2>

      <div class="recommended">
        <ProductCard
          v-for="(product, id) in inventory.slice(0, 3)"
          :key="id"
          class="card"
          :id="id"
          :product="product"
          :addToCart="addToCart"
          :sdtpc="sdtpc"
        />

      </div>
    </main>
  </div>
</template>

<script>
// @ is an alias to /src
// import HelloWorld from '@/components/HelloWorld.vue'
import ProductCard from '@/components/ProductCard.vue'

export default {
  name: 'HomeView',
  props: ['inventory', 'addToCart', 'sdtpc'], // receiver
  components: {
    ProductCard
  },
  methods: {

  },
  data () {
    return {

    }
  }
}
</script>
