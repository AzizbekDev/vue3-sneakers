<script setup>
import axios from "axios";
import { ref, computed, inject } from "vue";

import DrawerHeader from './DrawerHeader.vue'
import CartListItem from './CartListItem.vue'
import InfoBlock from './InfoBlock.vue'

const props = defineProps({
  totalPrice: Number,
  vatPrice: Number
})

const { cart } = inject('cart')
const isCreating = ref(false)
const orderId = ref(null)

const createOrder = async () => {
  try {
    isCreating.value = true

    const { data } = await axios.post('https://6e7baa9f3a425a05.mokky.dev/orders', {
      items: cart.value,
      totalPrice: props.totalPrice.value,
    })

    cart.value = []

    orderId.value = data.id

  } catch (err) {
    console.log(err)
  } finally {
    isCreating.value = false
  }
}

const cartIsEmpty = computed(() => cart.value.length === 0)

const disabledButton = computed(() => isCreating.value || cartIsEmpty.value)

</script>
<template>
  <div class="fixed top-0 left-0 h-full w-full bg-black z-10 opacity-70"></div>

  <div class="fixed top-0 right-0 h-full w-96 bg-white z-20 p-8">

    <DrawerHeader />
    <div v-if="!totalPrice || orderId" class="flex h-full items-center">
      <InfoBlock v-if='!totalPrice && !orderId' image-url="/package-icon.png" title="Корзина пустая"
        description="Добавьте хотя бы одну пару кроссовок, чтобы сделать заказ." />

      <InfoBlock v-if="orderId" image-url="/order-success-icon.png" title="Заказ оформлен!"
        :description="`Ваш заказ #${orderId} скоро будет передан курьерской доставке`" />
    </div>

    <div v-else>
      <CartListItem />

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

        <button :disabled="disabledButton" @click="createOrder"
          class="bg-lime-500 w-full rounded-xl py-3 mt-4 text-white disabled:bg-slate-300 hover:bg-lime-600 active:bg-lime-700 cursor-pointer">
          Оформить заказ
        </button>

      </div>

    </div>

  </div>

</template>
