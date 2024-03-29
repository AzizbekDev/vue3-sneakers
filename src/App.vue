<script setup>
import { onMounted, reactive, ref, provide, watch } from 'vue'
import axios from 'axios'

import Header from './components/Header.vue'
import CardList from './components/CardList.vue'
import Drawer from './components/Drawer.vue'

const items = ref([])

const cart = ref([])

const drawerOpen = ref(false)

const closeDrawer = () => {
  drawerOpen.value = false
}

const openDrawer = () => {
  drawerOpen.value = true
}

const filters = reactive({
  sortBy: 'name',
  searchQuery: ''
})

const onChangeSelect = (event) => {
  filters.sortBy = event.target.value
}

const onChangeSearchInput = (event) => {
  filters.searchQuery = event.target.value
}

const addToCart = (item) => {
    item.isAdded = true
    cart.value.push(item)
}

const removeFromCart = (item) => {
    item.isAdded = false
    cart.value.splice(cart.value.indexOf(item), 1)
}

const onClickAddPlus = (item) => {
  if(!item.isAdded){
    addToCart(item)
  }else{
    removeFromCart(item)
  }
}

const addToFavorite = async (item) => {
  try {
    if(!item.isFavorite){
      const obj = {
        parentId: item.id
      } 
      item.isFavorite = true
      const { data } = await axios.post('https://6e7baa9f3a425a05.mokky.dev/favorites', obj)
      item.favoridId = data.id
    } else {
      item.isFavorite = false
      await axios.delete(`https://6e7baa9f3a425a05.mokky.dev/favorites/${item.favoridId}`)
      item.favoriteId = null
    }
  } catch (err) {
    console.log(err)
  }
}

const fetchFavorites = async () => {
  try {
    const { data: favorites } = await axios.get('https://6e7baa9f3a425a05.mokky.dev/favorites')

    items.value = items.value.map((item) => {
      const favorite = favorites.find((favorite) => favorite.parentId === item.id)
      if (!favorite) {
        return item
      }
      return {
        ...item,
        isFavorite: true,
        favoridId: favorite.id
      }
    })
  } catch (err) {
    console.log(err)
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

    const { data } = await axios.get('https://6e7baa9f3a425a05.mokky.dev/items', {
      params
    })

    items.value = data.map((obj) => ({
      ...obj,
      isFavorite: false,
      favoriteId: null,
      isAdded: false
    }))
  } catch (err) {
    console.log(err)
  }
}

onMounted(async () => {
  await fetchItems()
  await fetchFavorites()
})

watch(filters, fetchItems)

provide('cart', {
  cart,
  closeDrawer,
  openDrawer,
  addToCart,
  removeFromCart
})
</script>
<template>
  <Drawer v-if="drawerOpen" />
  <div class="bg-white w-4/5 m-auto mt-14 rounded-xl shadow-xl">
    <Header @open-drawer="openDrawer" />
    <div class="p-10">
      <div class="flex justify-between items-center mb-8">
        <h2 class="text-3xl font-bold">Все кроссовки</h2>
        <div class="flex gap-4">
          <select id="selectFilter"
            @change="onChangeSelect"
            class="border rounded-md py-2 px-3 outline-none focus:border-gray-400"
          >
            <option value="name">По названию</option>
            <option value="price">По цене (дешевые)</option>
            <option value="-price">По цене (дорогие)</option>
          </select>
          <div class="relative">
            <img class="absolute left-4 top-3" src="/search.svg" alt="Search" />
            <input id="search"
              @input="onChangeSearchInput"
              class="border rounded-md py-2 pl-10 pr-4 outline-none focus:border-gray-400"
              type="text"
              placeholder="Поиск..."
            />
          </div>
        </div>
      </div>
      <CardList :items="items" @add-to-favorite="addToFavorite" @add-to-cart="onClickAddPlus" />
    </div>
  </div>
</template>
