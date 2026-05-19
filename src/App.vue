<script setup>
import { ref, onMounted, onUnmounted, onBeforeMount } from 'vue'

const products = ref([])
const isLoading = ref(true)
const error = ref(null)

// onMounted: runs AFTER the component is added to the page
// This is where you fetch data from APIs
onMounted(async () => {
  console.log('Component is now on the page!')
  
  try {
    // In Weeks 5-6, this will be a real API call:
    // const response = await fetch('/api/products')
    // products.value = await response.json()
    
    // For now, simulate a delay
    await new Promise(resolve => setTimeout(resolve, 1000))
    products.value = [
      { id: 1, name: 'White Bread', price: 60 },
      { id: 2, name: 'Chocolate Cake', price: 350 },
    ]
  } catch (err) {
    error.value = 'Failed to load products'
  } finally {
    isLoading.value = false
  }
})

// onUnmounted: runs when the component is removed from the page
// Clean up timers, event listeners, etc.
let intervalId
onMounted(() => {
  // Refresh dashboard data every 30 seconds
  intervalId = setInterval(() => {
    console.log('Refreshing data...')
  }, 5000)
})

onUnmounted(() => {
  // Clean up the interval when user leaves this page
  clearInterval(intervalId)
  console.log('Cleaned up!')
})
</script>

<template>
  <p v-if="isLoading">Loading products...</p>
  <p v-else-if="error" class="error">{{ error }}</p>
  <div v-else>
    <div v-for="product in products" :key="product.id">
      {{ product.name }}
    </div>
  </div>
</template>