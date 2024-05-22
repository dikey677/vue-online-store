<script setup>
import Header from './components/Header.vue'
import CardList from './components/CardList.vue'
import { onMounted, ref, watch, reactive, provide } from 'vue'
import axios from 'axios'
import Drawer from './components/Drawer.vue'

const items = ref([])
const cartItems = ref([])
const cartOpen = ref(false)

const filters = reactive({ sortBy: 'title', searchQuery: '' })

const onChangeSelect = (e) => {
  filters.sortBy = e.target.value
}

const onChangeSearch = (e) => {
  filters.searchQuery = e.target.value
}

const onCartOpen = () => {
  cartOpen.value = true
}

const onCartClose = () => {
  cartOpen.value = false
}

const fetchFavorites = async () => {
  try {
    const { data: favorites } = await axios.get('https://38b4994b47f6b2ae.mokky.dev/favorites')

    items.value = items.value.map((item) => {
      const favorite = favorites.find((favorite) => favorite.parentId === item.id)

      if (!favorite) {
        return item
      }
      return {
        ...item,
        isFavorite: true,
        favoriteId: favorite.id
      }
    })
  } catch (error) {
    console.log(error)
  }
}

const addToFavorite = async (item) => {
  if (!item.isFavorite) {
    try {
      const obj = {
        parentId: item.id
      }
      item.isFavorite = true
      const { data } = await axios.post('https://38b4994b47f6b2ae.mokky.dev/favorites', obj)

      item.favoriteId = data.id
      console.log(data)
    } catch (error) {
      console.log(error)
    }
  } else {
    item.isFavorite = false
    await axios.delete(`https://38b4994b47f6b2ae.mokky.dev/favorites/${item.favoriteId}`)

    item.favoriteId = null
  }
}

const addToCart = async (item) => {
  if (!item.isAdded) {
    cartItems.value.push(item)
    item.isAdded = true
    console.log(cartItems.value)
  } else {
    cartItems.value.splice(cartItems.value.indexOf(item), 1)
    item.isAdded = false
    console.log(cartItems.value)
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

    items.value = data.map((obj) => ({
      ...obj,
      isFavorite: false,
      isAdded: false,
      favoriteId: null
    }))

    fetchFavorites()
  } catch (error) {
    console.log(error)
  }
}

provide('cart', { cartItems, onCartClose })

onMounted(async () => {
  await fetchItems()
})

watch(filters, fetchItems)
</script>

<template>
  <Drawer v-if="cartOpen" />
  <div class="w-4/5 m-auto bg-white rounded-xl shadow-2xl mt-10">
    <Header @onCartOpen="onCartOpen" />

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
      <CardList :items="items" @addToFavorite="addToFavorite" @addToCart="addToCart" />
    </div>
  </div>
</template>
