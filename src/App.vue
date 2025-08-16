<script setup>
import { ref, provide } from 'vue'
import { RouterView } from 'vue-router'
import ToastMessage from './components/ToastMessage.vue'

const toastContent = ref('')
let toastTimeout = null

const showToast = (item) => {
  // 先清掉前一個 timeout
  if (toastTimeout) clearTimeout(toastTimeout)

  toastContent.value = item
  toastTimeout = setTimeout(() => {
    toastContent.value = ''
    toastTimeout = null
  }, 2000)
}

const closeToast = () => {
  toastContent.value = ''
  if (toastTimeout) {
    clearTimeout(toastTimeout)
    toastTimeout = null
  }
}

provide('showToast', showToast)
</script>

<template>
  <div class="relative">
    <RouterView />
    <div v-if="toastContent" class="absolute top-3 right-3">
      <ToastMessage @closeToast="closeToast">{{ toastContent }}</ToastMessage>
    </div>
  </div>
</template>
