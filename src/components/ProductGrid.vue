<template>
  <section class="w-full px-6 py-4 grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-6">
    <ProductCard
      v-for="p in products"
      :key="p.id"
      :product="p"
    />
  </section>
</template>

<script setup lang="ts">
import { ref } from 'vue'
import ProductCard from './ProductCard.vue'
interface Product { id: number; title: string; image: string; price: number }
const products = ref<Product[]>([
  { id: 1, title: 'Play Station 5',              image: '/ps5.png',                       price: 600 },
  { id: 2, title: 'Play Station Portal',         image: '/portal.png',                    price: 299 },
  { id: 3, title: 'Mando Dual Sense',            image: '/dualsense.png',                 price: 100 },
  { id: 4, title: 'Pedales Play Station',        image: '/pedals.png',                    price: 450 },
  { id: 5, title: 'DualSense 30th aniversario',  image: '/dualsense-anniversary.png',     price: 130 },
  { id: 6, title: 'Fifa 2025',                   image: '/fifa.png',                      price: 60 },
  { id: 7, title: 'Starfield',                   image: '/starfield.png',                 price: 80 },
  { id: 8, title: 'Horizon',                     image: '/horizon.png',                   price: 60 },
  { id: 9, title: 'GTA VI',                      image: '/gta.png',                       price: 119.99 }
])
</script>