<template>
  <div class="product  ">
    <div class="left">
      <img class="product-img" :src="props.product.image" alt="">
      <div class="product-info">
        <h1 class="product-title">
          {{props.product.title}}

        </h1>
        <span class="product-price">${{props.product.price.toFixed(2)}}</span>
      </div>
    </div>
    <button v-if="isPurchasedProduct(props.product.id) == false" @click="handleBuy" class="hover:bg-green-300 bg-green-500 p-1 rounded-lg cursor-pointer">Add fruit</button>
  </div>

</template>

<script setup>

import { defineProps, defineEmits } from 'vue';

const props = defineProps({
  product: Object,
  isPurchasedProduct: Function
})
const handleBuy = ()=>{
  emit('purchaseProductById', props.product)
}
const emit = defineEmits(['purchaseProductById'])
</script>

<style scoped>
.product{
   @apply
   max-w-[300px] w-full
   mt-3 bg-blue-100  rounded-lg p-2
   flex items-center  gap-3 justify-between
}
.left{
  @apply
  flex items-center gap-3 justify-center
}
.product-img{
  @apply
  w-12 h-12  rounded-full
}
.product-info{
  @apply
  flex flex-col gap-1.5
}
.product-title{
  @apply
  text-lg font-bold
}
.product-price{
  @apply
  text-sm font-normal
}
</style>
