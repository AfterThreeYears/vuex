<template>
  <ul>
    <li v-for="product in products">
      {{ product.title }} - {{ product.price | currency }}
      <br>
      <button
        :disabled="!product.inventory"
        @click="handleClick(product)">
        Add to cart
      </button>
    </li>
  </ul>
</template>

<script>
import { mapGetters, mapActions } from 'vuex'

export default {
  computed: mapGetters({
    products: 'products/allProducts'
  }),
  methods: {
    ...mapActions({
      addProductToCart: 'cart/addProductToCart',
      getAllProducts: 'products/getAllProducts'
    }),
    handleClick (product) {
      this.addProductToCart(product)
    }
  },
  created () {
    this.getAllProducts()
  }
}
</script>
