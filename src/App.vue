<script setup>
import { ref, reactive, computed } from 'vue';

// Primitive values
const productName = ref('White Bread')
const price = ref(60)
const isAvailable = ref(true)
const quantity = ref(0)

// To change a ref in JavaScript, use .value
function increasePrice() {
  price.value = price.value + 10
  // price is now 70, and the template updates automatically
}

///increasePrice() // Call the function to increase the price on the way to the template

// ref also works with objects and arrays
const product = ref({
  name: 'White Bread',
  price: 60,
  category: 'bread'
})
 product.value.price = 70 // Update the price in the product object

// reactive() for objects — no .value needed anywhere
const ingredient = reactive({
  name: 'Wheat Flour',
  currentStock: 50,
  reorderLevel: 20,
  unit: 'kg'
})

// Modify directly — no .value
function deductStock(amount) {
  ingredient.currentStock -= amount
}

// reactive() for arrays
const products = reactive([
  { id: 1, name: 'White Bread', price: 60 },
  { id: 2, name: 'Chocolate Cake', price: 350 },
])

function addProduct(product) {
  products.push(product)
}

</script>

<template>
   
  <div style="padding: 2rem;">
  <h1>Vue.js Fundamentals</h1>
    <p>This is our learning project. We'll build bakery features here.</p>

    <!-- In the template, NO .value needed — Vue unwraps it -->
    <h2>{{ productName }}</h2>
    <p>KES {{ price }}</p>
    <p>Available: {{ isAvailable ? 'Yes' : 'No' }}</p>
    <button @click="increasePrice">Increase Price</button>


      <p>{{ ingredient.name }}: {{ ingredient.currentStock }}{{ ingredient.unit }}</p>
      <button @click="deductStock(5)">Use 5kg</button>


      <H1>Text Interpolation for objects </H1>

       <h1>{{ product.name }}</h1>
      <p>KES {{ product.price }}</p>
      
      <!-- You can use JavaScript expressions inside {{ }} -->
      <p>{{ product.price * 1.16 }}</p>  <!-- Price with 16% VAT -->
      <p>{{ product.name.toUpperCase() }}</p>
      <p>{{ product.price > 100 ? 'Premium' : 'Standard' }}</p>
  </div>

</template>

<style scoped>

</style>
