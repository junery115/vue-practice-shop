<template>
  <div class="container">
    <div class="row">
      <div class="col-md-7">
        <div class="row">
          <div
            class="col-md-6"
            v-for="product in products"
            v-bind:key="product.id"
          >
            <product
              v-on:add-to-cart="addToCart(product)"
              :product="product"
              :isInCart="isInCart(product)"
            ></product>
          </div>
        </div>
      </div>
      <div class="col-md-5 my-5">
        <cart
          :items="cart"
          v-on:remove-from-cart="removeFromCart($event)"
          v-on:pay="pay()"
        ></cart>
      </div>
    </div>
  </div>
</template>

<script>
import products from '@/products.json'
import Product from '@/components/ProductComponent.vue'
import Cart from '@/components/CartComponent.vue'
export default {
  name: 'app',

  components: {
    Product,
    Cart,
  },
  data() {
    return {
      products,
      cart: [],
    }
  },
  methods: {
    addToCart(product) {
      this.cart.push(product)
    },

    isInCart(product) {
      const item = this.cart.find(item => item.id === product.id)
      if (item) {
        return true
      }
      return false
    },
    removeFromCart(product) {
      this.cart = this.cart.filter(item => item.id !== product.id)
    },
    pay() {
      this.cart = []
      alert('Shopping completed!')
    },
  },
}
</script>

<style>
body {
  background-color: #fbf8f3;
}
</style>
