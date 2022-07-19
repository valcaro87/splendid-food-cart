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

  <router-view :inventory="inventory" :addToCart="addToCart" :sdtpc="sendDataToProductCard" :pastorders="pastorders" />

  <SideBar
    v-if="sidebarVisible"
    :toggle = "ToggleSideBar"
    :cart = "cart"
    :inventory = "inventory"
    :removeproduct = "removeProduct"
    :sdts = "sendDataToSidebar"
    :checkOut = "checkOut"
    :pastorders = "pastorders"
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
      cart: {},
      pastorders: [],
      idz: 0
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
    addToCart (id, quantity) {
      if (!this.cart[id]) this.cart[id] = 0
      this.cart[id] += quantity // this.inventory[index].quantity
      // this.inventory[index].quantity = 0
      // console.log(this.cart[name]) // quantity
    },
    ToggleSideBar () {
      this.sidebarVisible = !this.sidebarVisible
    },
    removeProduct (key) {
      delete this.cart[key]
    },
    sendDataToSidebar () {
      return 'Checking out...'
    },
    sendDataToProductCard () {
      return 'Add to cart'
    },
    checkOut () {
      this.idz++
      // this.pastorders[this.idz] = this.cart
      // const curNum = this.idz
      const curCart = [this.cart]
      this.pastorders[this.idz] = JSON.stringify(curCart)
      // this.pastorders.push(this.pastorders[this.idz])
    },
    updated () {

    }
  }
}
</script>
