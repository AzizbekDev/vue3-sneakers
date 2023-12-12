<script setup>
import CartItem from './CartItem.vue'
import DrawerHeader from './DrawerHeader.vue'
</script>
<template>
  <div class="fixed top-0 left-0 h-screen w-full bg-black z-10 opacity-70"></div>
  <div class="fixed top-0 right-0 h-screen w-96 bg-white z-20 p-8">
    <DrawerHeader />
    <CartItem />
  </div>
</template>
