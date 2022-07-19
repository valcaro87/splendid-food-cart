<template>
  <main class="wrapper">
    <h1>Products</h1>

    <div class="card-container">
      <ProductCard
        v-for="(product, id) in inventory"
        :key="id"
        class="card"
        :id="id"
        :product="product"
        :addToCart="addToCart"
        :sdtpc = "sdtpc"
      />
    </div>

  </main>
</template>

<script>
import ProductCard from '@/components/ProductCard.vue'

export default {
  props: ['inventory', 'addToCart', 'sdtpc'],
  components: {
    ProductCard
  }
}
</script>
