<script setup>
const emit = defineEmits(['deleteFromCart'])

defineProps({
  title: String,
  imageUrl: String,
  price: Number
})
</script>

<template>
  <div class="flex items-centerw-full border border-slate-100 p-4 rounded-xl gap-4">
    <img :src="imageUrl" alt="Sneaker" class="w-16 h-16" />

    <div class="flex flex-col flex-1">
      <p>{{ title }}</p>

      <div class="flex justify-between mt-2">
        <b class="flex-1">{{ price }} руб.</b>
        <img
          @click="emit('deleteFromCart', item)"
          src="/public/close.svg"
          alt="Close"
          class="opacity-50 cursor-pointer hover:opacity-100 transition"
        />
      </div>
    </div>
  </div>
</template>
