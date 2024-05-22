<script setup>
import CartItem from './CartItem.vue'
import { inject } from 'vue'

const { cartItems, deleteFromCart } = inject('cart')
</script>

<template>
  <div class="flex flex-col gap-5">
    <CartItem
      v-for="cart in cartItems"
      :key="cart"
      :title="cart.title"
      :imageUrl="cart.imageUrl"
      :price="cart.price"
      @deleteFromCart="deleteFromCart(cart)"
    />
  </div>
</template>
