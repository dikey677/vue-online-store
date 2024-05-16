<script setup>
import Card from './Card.vue'

defineProps({
  items: Array
})

const onClickFavorite = () => {}
const onClickAdded = () => {}
</script>

<template>
  <div class="mt-10 grid grid-cols-4 gap-3">
    <Card
      v-for="item in items"
      :key="item.id"
      :title="item.title"
      :imageUrl="item.imageUrl"
      :price="item.price"
      :isFavorite="true"
      :isAdded="false"
      :onClickFavorite="onClickFavorite"
      :onClickAdded="onClickAdded"
    />
  </div>
</template>
