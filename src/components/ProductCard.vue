<template>
  <div class="bg-[#343655] rounded-lg overflow-hidden flex flex-col transition hover:scale-105">
    <div class="h-48 flex items-center justify-center bg-gray-700">
      <img
        :src="product.image"
        :alt="product.title"
        class="h-40 object-contain"
        @error="onError"
      />
    </div>
    <div class="p-4 flex-1 flex flex-col justify-between">
      <h3 class="text-white font-semibold mb-2">{{ product.title }}</h3>
      <div class="flex justify-between items-center">
        <span class="text-white font-bold">${{ product.price.toFixed(2) }}</span>
        <button class="bg-purple-600 hover:bg-purple-700 text-white px-4 py-2 rounded transition">
          Añadir
        </button>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { defineProps } from 'vue'
interface Product { id: number; title: string; image: string; price: number }
const { product } = defineProps<{ product: Product }>()
function onError(e: Event) {
  (e.target as HTMLImageElement).src = 'https://via.placeholder.com/400x300?text=No+Image'
}
</script>