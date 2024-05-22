<script setup>
import Card from './Card.vue'

defineProps({
  items: Array
})

const emit = defineEmits(['addToFavorite', 'onClickToAddCart'])
</script>

<template>
  <div class="mt-10 grid grid-cols-4 gap-3">
    <Card
      v-for="item in items"
      :key="item.id"
      :id="item.id"
      :title="item.title"
      :imageUrl="item.imageUrl"
      :price="item.price"
      :isFavorite="item.isFavorite"
      :onClickFavorite="() => emit('addToFavorite', item)"
      :onClickAdded="() => emit('onClickToAddCart', item)"
      :isAdded="item.isAdded"
    />
  </div>
</template>
