<template>
  <section class="w-full px-6 py-4">
    <p v-if="filteredProducts.length === 0" class="text-center text-white dark:text-gray-300 py-8">
      No se encontraron productos que coincidan con tu búsqueda.
    </p>
    <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-6">
      <ProductCard 
        v-for="product in filteredProducts" 
        :key="product.id" 
        :product="product"
        @add-to-cart="$emit('add-to-cart', $event)"
        @view-details="$emit('view-details', $event)"
      />
    </div>
  </section>
</template>

<script setup lang="ts">
import { computed } from 'vue';
import ProductCard from './ProductCard.vue';

interface Product {
  id: number;
  title: string;
  image: string;
  price: number;
  category: string;
}

interface Filter {
  priceMin?: number;
  priceMax?: number;
  categories?: {
    [key: string]: boolean;
  };
}

const props = defineProps({
  searchQuery: {
    type: String,
    default: ''
  },
  activeFilters: {
    type: Object as () => Filter,
    default: () => ({})
  }
});

defineEmits(['add-to-cart', 'view-details']);

const allProducts: Product[] = [
  {
    id: 1,
    title: 'Play Station 5',
    image: 'https://i.imgur.com/JDzGaYv.png',
    price: 600,
    category: 'consoles'
  },
  {
    id: 2,
    title: 'Play Station Portal',
    image: 'https://i.imgur.com/8XA4Oe6.png',
    price: 299,
    category: 'consoles'
  },
  {
    id: 3,
    title: 'Mando Dual Sense',
    image: 'https://i.imgur.com/YQmqJTM.png',
    price: 100,
    category: 'controllers'
  },
  {
    id: 4,
    title: 'Pedales Play Station',
    image: 'https://i.imgur.com/pYR8Vt0.png',
    price: 450,
    category: 'accessories'
  },
  {
    id: 5,
    title: 'Mando Dual Sense 30th aniversario',
    image: 'https://i.imgur.com/YQmqJTM.png',
    price: 130,
    category: 'controllers'
  },
  {
    id: 6,
    title: 'Fifa 2025',
    image: 'https://i.imgur.com/JGfIoF0.png',
    price: 60,
    category: 'games'
  },
  {
    id: 7,
    title: 'Starfield',
    image: 'https://i.imgur.com/K5sYlYN.png',
    price: 80,
    category: 'games'
  },
  {
    id: 8,
    title: 'Horizon',
    image: 'https://i.imgur.com/L8zBGwM.png',
    price: 60,
    category: 'games'
  },
  {
    id: 9,
    title: 'Grand Theft Auto VI',
    image: 'https://i.imgur.com/9XqLbZG.png',
    price: 119.99,
    category: 'games'
  }
];

const filteredProducts = computed(() => {
  let result = [...allProducts];
  
  // Aplicar búsqueda
  if (props.searchQuery) {
    const query = props.searchQuery.toLowerCase();
    result = result.filter(product => 
      product.title.toLowerCase().includes(query)
    );
  }
  
  // Aplicar filtros de precio
  if (props.activeFilters.priceMin !== undefined || props.activeFilters.priceMax !== undefined) {
    const min = props.activeFilters.priceMin || 0;
    const max = props.activeFilters.priceMax || Infinity;
    result = result.filter(product => 
      product.price >= min && product.price <= max
    );
  }
  
  // Aplicar filtros de categoría
  if (props.activeFilters.categories) {
    const categories = props.activeFilters.categories;
    const enabledCategories = Object.keys(categories).filter(key => categories[key]);
    
    if (enabledCategories.length > 0) {
      result = result.filter(product => 
        enabledCategories.includes(product.category)
      );
    }
  }
  
  return result;
});
</script>