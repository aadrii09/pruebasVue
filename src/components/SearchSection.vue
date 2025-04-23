<template>
  <section class="w-full px-6 py-4 flex justify-center">
    <div class="relative w-full max-w-md">
      <input
        v-model="query"
        type="text"
        placeholder="Buscar productos..."
        class="w-full bg-[#252540] border border-[#424567] text-white py-2 px-4 rounded-full focus:outline-none"
      />
      <button class="absolute right-3 top-1/2 transform -translate-y-1/2 text-gray-400">
        <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" fill="none"
             viewBox="0 0 24 24" stroke="currentColor">
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                d="M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0z"/>
        </svg>
      </button>
    </div>
  </section>
</template>

<script setup lang="ts">
import { ref } from 'vue'
const query = ref('')
</script>