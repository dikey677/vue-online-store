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
      title="Мужские Кроссовки Nike Blazer Mid Suede"
      image-url="/public/sneakers/sneakers-1.jpg"
      :price="12999"
      :isFavorite="true"
      :isAdded="false"
      :onClickFavorite="onClickFavorite"
      :onClickAdded="onClickAdded"
    />
  </div>
</template>
