<script setup>
defineProps({
    title: String,
    description: String,
    imageUrl: String,
});
</script>

<template>
    <div class="flex flex-col items-center text-center w-72 mx-auto">
        <img height="80" width="80" :src="imageUrl" alt="{{ title }}">
        <h2 class="mt-4 text-2xl font-medium">{{ title }}</h2>
        <p class="mt-2 text-gray-400">{{ description }}</p>
    </div>
</template>