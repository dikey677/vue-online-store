<script setup>
import DrawerHead from './DrawerHead.vue'
import CartListItems from './CartListItems.vue'
</script>

<template>
  <div class="fixed top-0 left-0 h-full w-full bg-black z-10 opacity-70"></div>
  <div class="fixed top-0 right-0 bg-white w-96 h-full z-20 p-8">
    <DrawerHead />
    <CartListItems />

    <div class="flex flex-col gap-5 my-7">
      <div class="flex gap-2">
        <span>Итого:</span>
        <div class="flex-1 border-b border-dashed"></div>
        <b>12999 ₽</b>
      </div>

      <div class="flex gap-2">
        <span>НДС 20%:</span>
        <div class="flex-1 border-b border-dashed"></div>
        <b>2300 ₽</b>
      </div>

      <button
        class="mt-5 bg-lime-500 w-full rounded-xl py-3 mb-6 text-white hover:bg-lime-600 active:bg-lime-700 disbled:bg-slate-400 cursor-pointer"
      >
        Оформить заказ
      </button>
    </div>
  </div>
</template>
