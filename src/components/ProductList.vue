<template>
  <div class="lg:w-[70%]">
    <h2 class="text-2xl font-semibold">商品列表</h2>
    <div class="flex w-full gap-2 flex-wrap justify-between py-8">
      <div
        class="flex flex-col w-[100%] sm:w-[48%] lg:w-[30%] mb-8 justify-between shadow-lg rounded-[5px] overflow-hidden"
        v-for="item in productData"
        :key="item.id"
      >
        <div>
          <img
            src="https://images.unsplash.com/photo-1546435770-a3e426bf472b?q=80&amp;w=2065&amp;auto=format&amp;fit=crop&amp;ixlib=rb-4.1.0&amp;ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D"
            alt="商品附圖"
            class="w-full"
          />
          <div class="flex flex-col gap-2 m-2">
            <h3 class="text-xl">{{ item.name }}</h3>
            <p>{{ item.des }}</p>
            <p class="text-blue-600">${{ item.price }}</p>
          </div>
        </div>
        <button
          @click="addProduct(item)"
          type="button"
          class="text-white bg-success hover:bg-green-500 active:bg-green-800 p-2 rounded-[4px] m-2"
        >
          加入購物車
        </button>
      </div>
    </div>
  </div>
</template>
<script setup>
import { inject } from 'vue'

const showToast = inject('showToast')

defineProps({
  productData: {
    type: Array,
  },
})

const emit = defineEmits(['addProduct'])

const addProduct = (item) => {
  emit('addProduct', item)
  showToast(`商品 "${item.name}" 已加入購物車`)
}
</script>
