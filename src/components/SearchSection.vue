<template>
  <section class="w-full px-6 py-4 flex flex-col md:flex-row justify-between items-center">
    <div class="relative w-full max-w-md mb-4 md:mb-0">
      <div class="absolute inset-y-0 left-3 flex items-center pointer-events-none">
        <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 text-gray-500" viewBox="0 0 20 20" fill="currentColor">
          <path fill-rule="evenodd" d="M8 4a4 4 0 100 8 4 4 0 000-8zM2 8a6 6 0 1110.89 3.476l4.817 4.817a1 1 0 01-1.414 1.414l-4.816-4.816A6 6 0 012 8z" clip-rule="evenodd" />
        </svg>
      </div>
      <input 
        v-model="searchQuery"
        @keyup.enter="handleSearch"
        type="text" 
        placeholder="Buscar en PixelVault o escribir una URL" 
        class="w-full pl-10 pr-4 py-2 rounded-full bg-[#d9d9d9] dark:bg-gray-700 dark:text-white text-gray-800 focus:outline-none"
      />
    </div>
    
    <div class="relative">
      <button @click="showFilters = !showFilters" class="ml-4 px-6 py-2 bg-primary-light dark:bg-gray-700 text-white rounded-md flex items-center hover:bg-opacity-90 transition-colors">
        <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 mr-2" fill="none" viewBox="0 0 24 24" stroke="currentColor">
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16M4 18h7" />
        </svg>
        Filtrar
      </button>
      
      <Transition name="slide-fade">
        <div v-if="showFilters" class="absolute right-0 mt-2 w-64 bg-white dark:bg-gray-800 rounded-lg shadow-lg p-4 z-10">
          <h3 class="font-bold text-gray-800 dark:text-white mb-3">Filtros</h3>
          
          <div class="mb-4">
            <label class="block text-sm text-gray-700 dark:text-gray-300 mb-1">Precio</label>
            <div class="flex items-center">
              <input v-model="filters.priceMin" type="number" min="0" class="w-20 p-1 border rounded dark:bg-gray-700 dark:text-white" />
              <span class="mx-2 text-gray-500">-</span>
              <input v-model="filters.priceMax" type="number" min="0" class="w-20 p-1 border rounded dark:bg-gray-700 dark:text-white" />
            </div>
          </div>
          
          <div class="mb-4">
            <label class="block text-sm text-gray-700 dark:text-gray-300 mb-1">Categorías</label>
            <div class="space-y-1">
              <div class="flex items-center">
                <input v-model="filters.categories.consoles" type="checkbox" id="consoles" class="mr-2" />
                <label for="consoles" class="text-sm text-gray-700 dark:text-gray-300">Consolas</label>
              </div>
              <div class="flex items-center">
                <input v-model="filters.categories.controllers" type="checkbox" id="controllers" class="mr-2" />
                <label for="controllers" class="text-sm text-gray-700 dark:text-gray-300">Mandos</label>
              </div>
              <div class="flex items-center">
                <input v-model="filters.categories.games" type="checkbox" id="games" class="mr-2" />
                <label for="games" class="text-sm text-gray-700 dark:text-gray-300">Juegos</label>
              </div>
              <div class="flex items-center">
                <input v-model="filters.categories.accessories" type="checkbox" id="accessories" class="mr-2" />
                <label for="accessories" class="text-sm text-gray-700 dark:text-gray-300">Accesorios</label>
              </div>
            </div>
          </div>
          
          <div class="flex justify-end">
            <button @click="showFilters = false" class="px-3 py-1 text-sm text-gray-600 dark:text-gray-300 mr-2">Cancelar</button>
            <button @click="applyFilters" class="px-3 py-1 text-sm bg-accent text-white rounded">Aplicar</button>
          </div>
        </div>
      </Transition>
    </div>
  </section>
</template>

<script setup lang="ts">
import { ref } from 'vue';

interface Filters {
  priceMin: number;
  priceMax: number;
  categories: {
    consoles: boolean;
    controllers: boolean;
    games: boolean;
    accessories: boolean;
    [key: string]: boolean;
  };
}

const emit = defineEmits(['search', 'filter']);

const searchQuery = ref('');
const showFilters = ref(false);
const filters = ref<Filters>({
  priceMin: 0,
  priceMax: 1000,
  categories: {
    consoles: true,
    controllers: true,
    games: true,
    accessories: true
  }
});

const handleSearch = () => {
  emit('search', searchQuery.value);
};

const applyFilters = () => {
  emit('filter', filters.value);
  showFilters.value = false;
};
</script>