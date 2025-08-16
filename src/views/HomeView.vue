<template>
  <div class="max-w-[1296px] mx-auto flex flex-col justify-center lg:flex-row gap-8 p-8">
    <ProductList :productData="productData" @addProduct="addProduct" />
    <ShopCart :cartData="cartData" :total="total" @removeItem="removeItem" />
  </div>
</template>
<script setup>
import { computed, ref } from 'vue'
import ProductList from '@/components/ProductList.vue'
import ShopCart from '@/components/ShopCart.vue'

const productData = ref([
  { id: 1, name: '耳罩式藍芽耳機', des: '舒適配戴，支援降噪技術', price: 2490 },
  { id: 2, name: '耳罩式彩虹耳機', des: '舒適配戴，支援降噪技術', price: 1380 },
  { id: 3, name: '時尚藍芽耳機', des: '舒適配戴，支援降噪技術', price: 7990 },
  { id: 4, name: '機械式鍵盤', des: '紅軸機械鍵盤，打字手感極佳', price: 1890 },
  { id: 5, name: '無線滑鼠', des: '靜音按鍵設計，長效電池', price: 890 },
])

const cartData = ref([
  { id: 1, name: '耳罩式藍芽耳機', des: '舒適配戴，支援降噪技術', price: 2490, quantity: 1 },
])

const total = computed(() => {
  return cartData.value.reduce((total, item) => total + item.price * item.quantity, 0)
})

const addProduct = (item) => {
  const existingIndex = cartData.value.findIndex((p) => p.id === item.id)
  if (existingIndex !== -1) {
    cartData.value[existingIndex].quantity += 1
  } else {
    cartData.value.push({ ...item, quantity: 1 })
  }
}

const removeItem = (item) => {
  const itemIndex = cartData.value.findIndex((p) => p.id === item.id)
  if (itemIndex !== -1) {
    cartData.value = cartData.value.filter((p) => p.id !== item.id)
  }
}
</script>
