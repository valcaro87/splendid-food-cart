<template>
  <header class="top-bar spread">
    <nav class="top-bar-nav">
      <router-link to="/" class="top-bar-link">
        <i class="icofont-spoon-and-fork"></i>
        <span>Home</span>
      </router-link>
      <router-link to="/products" class="top-bar-link">
        <span>Products</span>
      </router-link>
      <router-link to="/past-orders" class="top-bar-link">
        <span>Past Orders</span>
      </router-link>
    </nav>

    <div @click="ToggleSideBar" class="top-bar-cart-link">
      <i class="icofont-cart-alt icofont-1x"></i>
      <span> ( {{ totalItems }} ) </span>
    </div>

  </header>

  <router-view :inventory="inventory" :addToCart="addToCart" />

  <SideBar
    v-if="sidebarVisible"
    :toggle="ToggleSideBar"
    :cart="cart"
    :inventory="inventory"
    :removeproduct="removeProduct"
  />

</template>

<style scope>
/* scope only affects local file, not global */

</style>

<script>
import SideBar from '@/components/SideBar.vue'
import food from './food.json'

export default {
  components: {
    SideBar
  },
  data () {
    return {
      sidebarVisible: true,
      inventory: food,
      cart: {}
    }
  },
  computed: {
    totalItems () {
      return Object.values(this.cart).reduce((acc, curr, index) => {
        return acc + curr
      }, 0)
    }
  },
  methods: {
    addToCart (name, quantity) {
      if (!this.cart[name]) this.cart[name] = 0
      this.cart[name] += quantity // this.inventory[index].quantity
      // this.inventory[index].quantity = 0
      // console.log(this.cart[name]) // quantity
    },
    ToggleSideBar () {
      this.sidebarVisible = !this.sidebarVisible
    },
    removeProduct (key) {
      delete this.cart[key]
    }
  }
}
</script>
