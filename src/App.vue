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
    <div @click="toggleSidebar" class="top-bar-cart-link">
      <i class="icofont-cart-alt icofont-1x"></i>
      <span>Cart ({{ totalQuantity }})</span>
    </div>
  </header>
  <router-view
    :inventory="inventory"
    :addToCart="addToCart"
  />

  <Sidebar
    v-if="showSidebar"
    :toggle="toggleSidebar"
    :cart="cart"
    :inventory="inventory"
    :remove="removeItem"
  />

</template>
<script>
import 'intro.js/minified/introjs.min.css'
import 'intro.js/themes/introjs-modern.css'
import Sidebar from '@/components/Sidebar.vue'
import food from '@/food.json'
import introJs from 'intro.js'

export default {
  components: {
    Sidebar
  },
  data () {
    return {
      showSidebar: false,
      inventory: food,
      cart: {}
    }
  },
  computed: {
    totalQuantity () {
      return Object.values(this.cart).reduce((acc, curr) => {
        return acc + curr
      }, 0)
    }
  },
  methods: {
    addToCart (name, quantity) {
      if (!this.cart[name]) this.cart[name] = 0
      this.cart[name] += quantity
      console.log(this.cart)
    },
    toggleSidebar () {
      this.showSidebar = !this.showSidebar
    },
    removeItem (name) {
      delete this.cart[name]
    }
  },
  mounted () {
    const intro = introJs()
    intro.setOptions({
      steps: [
        {
          element: '.top-bar-nav',
          intro: 'This is the navigation bar. Click here to access different pages.'
        },
        {
          element: '.top-bar-cart-link',
          intro: 'This is the cart. It contains all of the items that you have selected to purchase.'
        }
      ],
      nextToDone: true
    })
    intro.start()
  }
}
</script>
