<template>
  <div class="cart">
    <h2>Your Cart</h2>
    <p v-show="!products.length"><i>Please add some products to cart.</i></p>
    <ul>
      <li v-for="product in products">
        {{ product.title }} - {{ product.price | currency }} x {{ product.quantity }}
      </li>
    </ul>
    <p>Total: {{ total | currency }}</p>
    <p><button :disabled="!products.length" @click="checkout(products)">Checkout</button></p>
    <p v-show="checkoutStatus">Checkout {{ checkoutStatus }}.</p>
  </div>
</template>

<script>
  import { mapGetters, mapState } from 'vuex'
  export default {
    computed: {
      // mapState 函数返回的是一个对象，...是展开运算符
      ...mapState({
        checkoutStatus: state => state.cart.checkoutStatus
      }),
      ...mapGetters('cart', {
        products: 'cartProducts',
        total: 'cartTotalPrice'
      })
    },
    methods: {
      checkout (products) {
        this.$store.dispatch('cart/checkout', products)
      }
    }
  }
</script>
