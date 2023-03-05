<template>
  <div id="wrapper">
    <div class="header ">
      <h1 class="main-title text-blue-400 text-2xl">Alışveriş Sepeti Uygulaması - {{wallet}} $</h1>
      <p1 class="purchased-count-text text-center">Şu ana kadar {{purchasedProduct.length}} tane ürün aldınız...</p1>

    </div>
   <div class="product-list">
     <app-product-item
         v-for="product in products" :key="product.id"
         :product="product" @purchaseProductById="purchadeProductById"
         :isPurchasedProduct="isPurchasedProduct"
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

const wallet = ref(250.0)
 const purchasedProduct =ref([])
 const purchadeProductById = (product)=>{
  purchasedProduct.value.push(product)
 }

 const isPurchasedProduct = (id) =>{
  const product = purchasedProduct.value.find(
      (purchasedProductItem) => purchasedProductItem.id == id
  );
  if(product){
    return true;
  } else{
    return false;
  }


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
