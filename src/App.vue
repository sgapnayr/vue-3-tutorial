<!-- eslint-disable @typescript-eslint/no-unused-vars -->
<script setup lang="ts">
import { ref, computed } from 'vue'

interface Product {
  productId: string
  productName: string
  productPrice: string
  productDescription: string
  productImage: string // URL to the product image
  productCategory: string // Category of the product
  productStock: number // Quantity in stock
  productRating: number // Average rating (e.g., out of 5)
  productWeight: string // Weight of the product
  productDimensions: string // Dimensions of the product
  manufacturer: string // Manufacturer of the product
  releaseDate: string // Release/Manufacturing date
  productTags: string[] // Tags for search optimization
}

const inventoryData: Product[] = [
  {
    productId: '1',
    productName: 'Candle',
    productPrice: '4.99',
    productDescription: 'Light smell, lights for 4 hours',
    productImage: 'url_to_candle_image.jpg',
    productCategory: 'Home Decor',
    productStock: 150,
    productRating: 4.5,
    productWeight: '200g',
    productDimensions: '5x5x10 cm',
    manufacturer: 'Candle Co',
    releaseDate: '2021-03-15',
    productTags: ['candle', 'light', 'decor']
  },
  {
    productId: '2',
    productName: 'Pencil',
    productPrice: '1.99',
    productDescription: 'Writes #2 lead',
    productImage: 'url_to_pencil_image.jpg',
    productCategory: 'Stationery',
    productStock: 500,
    productRating: 4.0,
    productWeight: '10g',
    productDimensions: '0.5x0.5x17 cm',
    manufacturer: 'Pencil Inc',
    releaseDate: '2020-08-01',
    productTags: ['pencil', 'writing', 'school']
  }
]

const fetchedData = ref()
const buttonState = ref<'idle' | 'loading' | 'success' | 'failed' | 'disable'>('idle')

function fetchData() {
  buttonState.value = 'loading'

  setTimeout(() => {
    fetchedData.value = inventoryData
    buttonState.value = 'success'
  }, 2500)

  setTimeout(() => {
    buttonState.value = 'idle'
  }, 5000)
}

const buttonStats = computed(() => {
  return buttonState.value === 'success'
    ? 'Successful Fetch.'
    : buttonState.value === 'loading'
      ? 'Loading...'
      : 'Fetch Data'
})
</script>

<template>
  <div class="content-wrapper">
    <button class="button-class" @click="fetchData">{{ buttonStats }}</button>

    {{ fetchedData }}
  </div>
</template>

<style scoped>
.content-wrapper {
  width: 100%;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.button-class {
  background-color: #42b883;
  color: white;
  padding: 1rem 2rem;
  border-radius: 16px;
  outline: none;
  border: none;
  cursor: pointer;
}

.button-class:active {
  opacity: 0;
}
</style>
