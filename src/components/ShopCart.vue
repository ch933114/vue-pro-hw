<template>
  <div class="lg:w-[30%]">
    <h2 class="text-2xl font-semibold">購物車</h2>
    <div class="flex flex-col gap-2 py-8">
      <div
        v-for="item in cartData"
        :key="item.id"
        class="bg-white rounded-[2px] flex justify-between items-center px-6 py-2 shadow-lg border border-gray-100"
      >
        <div>
          <p>{{ item.name }}</p>
          <p class="text-gray-400">數量 : {{ item.quantity }}</p>
        </div>
        <div class="flex gap-3 items-center">
          <p>${{ item.price * item.quantity }}</p>
          <button
            type="button"
            @click="removeItem(item)"
            class="bg-danger text-white py-1 px-2 rounded-[2px] hover:bg-red-300"
          >
            移除
          </button>
        </div>
      </div>
    </div>
    <div class="text-right text-xl font-bold">總金額 : $ {{ total }}</div>
  </div>
</template>
<script setup>
defineProps({
  cartData: {
    type: Array,
  },
  total: {
    type: Number,
  },
})

const emit = defineEmits(['removeItem'])

const removeItem = (item) => {
  emit('removeItem', item)
}
</script>
