<script setup>
import Header from './components/Header.vue'
import CardList from './components/CardList.vue'
import { onMounted, ref, watch, reactive } from 'vue'
import axios from 'axios'
// import Drawer from './components/Drawer.vue'

const items = ref([])

const filters = reactive({ sortBy: 'title', searchQuery: '' })

const onChangeSelect = (e) => {
  filters.sortBy = e.target.value
  // console.log(e.target.value)
}

const onChangeSearch = (e) => {
  filters.searchQuery = e.target.value
  // console.log(e.target.value)
}

const fetchFavorites = async () => {
  try {
    const { data } = await axios.get('https://38b4994b47f6b2ae.mokky.dev/favorites')

    items.value = data.map((obj) => ({ ...obj, isFavorite: false, isAdded: false }))
  } catch (error) {
    console.log(error)
  }
}

const fetchItems = async () => {
  try {
    const params = {
      sortBy: filters.sortBy
    }

    if (filters.searchQuery) {
      params.title = `*${filters.searchQuery}*`
    }

    const { data } = await axios.get('https://38b4994b47f6b2ae.mokky.dev/items', { params })

    items.value = data
  } catch (error) {
    console.log(error)
  }
}

onMounted(fetchItems)
watch(filters, fetchItems)
</script>

<template>
  <!-- <Drawer /> -->
  <div class="w-4/5 m-auto bg-white rounded-xl shadow-2xl mt-10">
    <Header />

    <div class="p-10">
      <div class="flex justify-between">
        <h2 class="text-3xl font-bold">Все кроссовки</h2>

        <div class="flex gap-4">
          <select @change="onChangeSelect" class="py-2 px-3 border rounded-md outline-none">
            <option value="name">По названию</option>
            <option value="price">Дешевле</option>
            <option value="-price">Дороже</option>
          </select>

          <div class="relative">
            <img src="/public/search.svg" class="absolute top-3 left-4" />
            <input
              @input="onChangeSearch"
              type="text"
              placeholder="Поиск..."
              class="border rounded-md py-2 pl-11 pr-4 outline-none focus:border-gray-400 hover:border-gray-400 transition"
            />
          </div>
        </div>
      </div>
      <CardList :items="items" />
    </div>
  </div>
</template>
