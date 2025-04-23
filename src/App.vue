<template>
  <div class="min-h-screen flex flex-col bg-gradient-to-b from-[#1f2034] to-[#252540]">
    <TheHeader/>
    <HeroSection/>
    <SearchSection/>
    <ProductGrid/>
    <TheFooter/>
  </div>
</template>

<script setup lang="ts">
import TheHeader     from './components/TheHeader.vue'
import HeroSection   from './components/HeroSection.vue'
import SearchSection from './components/SearchSection.vue'
import ProductGrid   from './components/ProductGrid.vue'
import TheFooter     from './components/TheFooter.vue'
</script>