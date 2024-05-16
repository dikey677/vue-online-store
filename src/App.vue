<script setup>
import Header from './components/Header.vue'
import CardList from './components/CardList.vue'
import { onMounted } from 'vue'

// import Drawer from './components/Drawer.vue'

onMounted(() => {})
</script>

<template>
  <!-- <Drawer /> -->
  <div class="w-4/5 m-auto bg-white rounded-xl shadow-2xl mt-10">
    <Header />

    <div class="p-10">
      <div class="flex justify-between">
        <h2 class="text-3xl font-bold">Все кроссовки</h2>

        <div class="flex gap-4">
          <select class="py-2 px-3 border rounded-md outline-none">
            <option>По названию</option>
            <option>Дешевле</option>
            <option>Дороже</option>
          </select>

          <div class="relative">
            <img src="/public/search.svg" class="absolute top-3 left-4" />
            <input
              type="text"
              placeholder="Поиск..."
              class="border rounded-md py-2 pl-11 pr-4 outline-none focus:border-gray-400 hover:border-gray-400 transition"
            />
          </div>
        </div>
      </div>
      <CardList />
    </div>
  </div>
</template>
