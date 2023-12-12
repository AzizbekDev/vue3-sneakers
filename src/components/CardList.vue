<script setup>
import Card from './Card.vue'
</script>
<template>
  <div class="grid grid-cols-4 gap-5">
    <Card
      title="Мужские Кроссовки Nike Blazer Mid Suede"
      imageUrl="/sneakers/sneakers-1.jpg"
      :price="12999"
    />
    <Card
      title="Мужские Кроссовки Nike Air Max 270"
      imageUrl="/sneakers/sneakers-2.jpg"
      :price="12999"
      isAdded
      isFavorite
    />
    <Card
      title="Мужские Кроссовки Nike Blazer Mid Suede"
      imageUrl="/sneakers/sneakers-3.jpg"
      :price="8499"
    />
    <Card
      title="Кроссовки Puma X Aka Boku Future Rider"
      imageUrl="/sneakers/sneakers-4.jpg"
      :price="8499"
      isFavorite
    />
    <Card
      title="Мужские Кроссовки Under Armour Curry 8"
      imageUrl="/sneakers/sneakers-5.jpg"
      :price="15199"
    />
    <Card
      title="Мужские Кроссовки Nike Kyrie 7"
      imageUrl="/sneakers/sneakers-6.jpg"
      :price="10799"
    />
    <Card
      title="Мужские Кроссовки Jordan Air Jordan 11"
      imageUrl="/sneakers/sneakers-7.jpg"
      :price="11299"
      isFavorite
    />
    <Card
      title="Мужские Кроссовки Nike LeBron XVIII"
      imageUrl="/sneakers/sneakers-8.jpg"
      :price="10799"
    />
    <Card
      title="Мужские Кроссовки Nike Lebron XVIII Low"
      imageUrl="/sneakers/sneakers-9.jpg"
      :price="16499"
      isFavorite
    />
    <Card
      title="Мужские Кроссовки Nike Blazer Mid Suede"
      imageUrl="/sneakers/sneakers-10.jpg"
      :price="8499"
    />
    <Card
      title="Кроссовки Puma X Aka Boku Future Rider"
      imageUrl="/sneakers/sneakers-11.jpg"
      :price="13999"
    />
    <Card
      title="Мужские Кроссовки Nike Kyrie Flytrap IV"
      imageUrl="/sneakers/sneakers-12.jpg"
      :price="8499"
    />
  </div>
</template>
