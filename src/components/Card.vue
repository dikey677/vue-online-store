<script setup>
defineProps({
  title: String,
  imageUrl: String,
  price: Number,
  isFavorite: Boolean,
  isAdded: Boolean,
  onClickFavorite: Function,
  onClickAdded: Function
})
</script>

<template>
  <div>
    <div
      class="bg-white relative border border-slate-100 rounded-xl p-8 cursor-pointer hover:-translate-y-2 hover:shadow-2xl transition"
    >
      <img
        :src="!isFavorite ? './public/like-1.svg' : './public/like-2.svg'"
        alt="Like"
        class="absolute top-8 left-8"
        @click="onClickFavorite"
      />
      <img :src="imageUrl" alt="Sneaker" />
      <p class="mt-2">{{ title }}</p>

      <div class="flex justify-between mt-5">
        <div class="flex flex-col">
          <span class="text-slate-400 uppercase">Цена:</span>
          <b>{{ price }} руб.</b>
        </div>

        <img
          :src="!isAdded ? './public/plus.svg' : './public/checked.svg'"
          alt="Add"
          @click="onClickAdded"
        />
      </div>
    </div>
  </div>
</template>
