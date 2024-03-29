<script setup>
defineProps({
  id: Number,
  title: String,
  price: Number,
  imageUrl: String
})
</script>

<template>
  <div class="flex items-center gap-5 border border-slate-100 rounded-xl p-4">
    <img class="w-16 h-16" :src="imageUrl" :alt="title" />
    <div class="flex flex-col">
      <p>{{ title }}</p>
      <div class="flex justify-between">
        <b>{{ price }} руб.</b>
        <img class="opacity-50 transition hover:opacity-100" src="/close.svg" alt="Close" />
      </div>
    </div>
  </div>
</template>
