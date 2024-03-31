<script setup>
const emit = defineEmits(['openDrawer'])
defineProps({
  totalPrice: Number
})
</script>

<template>
  <header class="flex justify-between border-b border-slate-200 px-10 py-8">

    <RouterLink to="/">
      <div class="flex items-center gap-4">
        <img class="w-10" src="/logo.png" alt="Logo" />
        <div>
          <h2 class="text-xl font-bold uppercase">Vue Sneakers</h2>
          <p class="text-slate-400">Магазин лучших кроссовок</p>
        </div>
      </div>
    </RouterLink>

    <ul class="flex items-center gap-10">
      <li @click="() => emit('openDrawer')"
        class="flex items-center gap-2 text-gray-500 hover:text-black cursor-pointer">
        <img src="/cart.svg" alt="Cart" />
        <b>{{ totalPrice }} руб.</b>
      </li>
      <RouterLink to="/favorites">
        <li class="flex items-center gap-2 text-gray-500 hover:text-black cursor-pointer">
          <img src="/heart.svg" alt="Heart" />
          <span>Закладки</span>
        </li>
      </RouterLink>
      <li class="flex items-center gap-2 text-gray-500 hover:text-black cursor-pointer">
        <img src="/profile.svg" alt="Profile" />
        <span>Профиль</span>
      </li>
    </ul>
  </header>
</template>
