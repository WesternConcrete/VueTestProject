<template>
    <main class="wrapper">
        <h1>Products</h1>
        <div class="card-container">
            <ProductCard
                v-for="product in inventory"
                :key="product.id"
                class="card"
                :product="product"
                :addToCart="addToCart"
            />
        </div>
    </main>
</template>

<script>
import ProductCard from '@/components/ProductCard.vue'

export default {
  name: 'Products',
  props: ['inventory', 'addToCart'],
  components: {
    ProductCard
  }
}
</script>
