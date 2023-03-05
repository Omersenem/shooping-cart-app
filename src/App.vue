<template>
  <div id="wrapper">
    <div class="header flex flex-col">
      <h1 class="main-title text-blue-400 text-2xl">Alışveriş Sepeti Uygulaması - {{wallet.toFixed(2)}} $</h1>
      <p1 class="purchased-count-text text-center">Şu ana kadar {{purchasedProduct.length}} tane ürün aldınız...</p1>
      <button @click="wallet +=5" class="bg-blue-100 mx-32 rounded-lg hover:bg-red-200" >Para ekle +5$</button>
    </div>
   <div class="product-list">
     <app-product-item
         v-for="product in products" :key="product.id"
         :product="product" @purchaseProductById="purchadeProductById"
         :isPurchasedProduct="isPurchasedProduct"
         @sellProductById="sellProductById"
     ></app-product-item>
   </div>
    <pre>
      {{purchasedProduct}}
    </pre>
  </div>

</template>

<script setup>
 import { products } from '@/constants/data'
import AppProductItem from "@/components/appProductItem.vue";
import {ref} from "vue";

const wallet = ref(5.00)
 const purchasedProduct =ref([])

 const purchadeProductById = (product)=>{

 if(wallet.value >= product.price){
   wallet.value -= product.price;
   purchasedProduct.value.push(product)
 }
 else{
   alert('Yetersiz Bakiye')
 }
 }
 const sellProductById = ({id,price})=>{
   wallet.value += price;

   purchasedProduct.value = purchasedProduct.value.filter((purchasedProductItem) => purchasedProductItem.id != id)
 }

 const isPurchasedProduct = (id) =>{
  const product = purchasedProduct.value.find(
      (purchasedProductItem) => purchasedProductItem.id == id
  );
  return !!product;

 }

</script>

<style scoped>
body{
  font-family: ".SF NS Mono",serif !important;
  background-color: #f1f1f1;
}
#wrapper{
  @apply
  flex items-center justify-center flex-col mt-5
}
.product-list{
  @apply
  flex items-center justify-center gap-3 flex-wrap
}
</style>
