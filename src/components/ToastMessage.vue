<template>
  <div class="flex gap-6 text-white justify-between bg-success p-4 rounded-[5px]">
    <slot>這是通知訊息</slot>
    <button @click="closeToast">x</button>
  </div>
</template>
<script setup>
const emit = defineEmits(['closeToast'])

const closeToast = () => {
  emit('closeToast')
}
</script>
