<script setup>
import DrawerHeader from './DrawerHeader.vue'
import CartListItem from './CartListItem.vue'
import InfoBlock from './InfoBlock.vue'

defineProps({
  totalPrice: Number,
  vatPrice: Number,
  disabledButton: Boolean
})

const emit = defineEmits(['createOrder'])

</script>
<template>
  <div class="fixed top-0 left-0 h-full w-full bg-black z-10 opacity-70"></div>

  <div class="fixed top-0 right-0 h-full w-96 bg-white z-20 p-8">

    <DrawerHeader />

    <CartListItem />

    <div v-if="!totalPrice" class="flex h-full items-center">
      <InfoBlock image-url="/package-icon.png" title="Корзина пустая"
        description="Добавьте хотя бы одну пару кроссовок, чтобы сделать заказ." />
    </div>

    <div v-else>
      <div class="flex flex-col gap-4 mt-7">

        <div class="flex gap-2">
          <span>Итого:</span>
          <div class="flex-1 border-b border-dashed"></div>
          <b>{{ totalPrice }} руб.</b>
        </div>

        <div class="flex gap-2">
          <span>Налог 5%:</span>
          <div class="flex-1 border-b border-dashed"></div>
          <b>{{ vatPrice }} руб. </b>
        </div>

        <button :disabled="disabledButton" @click="emit('createOrder')"
          class="bg-lime-500 w-full rounded-xl py-3 mt-4 text-white disabled:bg-slate-300 hover:bg-lime-600 active:bg-lime-700 cursor-pointer">
          Оформить заказ
        </button>

      </div>
    </div>

  </div>

</template>
