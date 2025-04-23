<template>
  <div class="min-h-screen bg-gradient-to-b from-primary-dark to-secondary dark:from-gray-900 dark:to-black">
    <TheHeader :cartCount="cartCount" @toggle-cart="showCart = !showCart" />
    <HeroSection />
    <SearchSection @search="handleSearch" @filter="handleFilter" />
    <ProductGrid 
      :searchQuery="searchQuery" 
      :activeFilters="activeFilters" 
      @add-to-cart="addToCart"
      @view-details="viewProductDetails"
    />
    <TheFooter />
    
    <Transition name="fade">
      <Cart 
        v-if="showCart" 
        :items="cartItems" 
        @close="showCart = false"
        @remove-item="removeFromCart"
        @update-quantity="updateQuantity"
        @checkout="checkout"
      />
    </Transition>
    
    <Transition name="fade">
      <ProductDetails 
        v-if="selectedProduct" 
        :product="selectedProduct" 
        @close="selectedProduct = null"
        @add-to-cart="addToCart"
      />
    </Transition>
    
    <button @click="toggleDarkMode" class="fixed bottom-4 right-4 bg-white dark:bg-gray-800 p-2 rounded-full shadow-lg z-10">
      <svg v-if="darkMode" xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 text-yellow-500" fill="none" viewBox="0 0 24 24" stroke="currentColor">
        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 3v1m0 16v1m9-9h-1M4 12H3m15.364 6.364l-.707-.707M6.343 6.343l-.707-.707m12.728 0l-.707.707M6.343 17.657l-.707.707M16 12a4 4 0 11-8 0 4 4 0 018 0z" />
      </svg>
      <svg v-else xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 text-gray-700" fill="none" viewBox="0 0 24 24" stroke="currentColor">
        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M20.354 15.354A9 9 0 018.646 3.646 9.003 9.003 0 0012 21a9.003 9.003 0 008.354-5.646z" />
      </svg>
    </button>
  </div>
</template>

<script setup lang="ts">
import { ref, computed, onMounted } from 'vue';
import TheHeader from './components/TheHeader.vue';
import HeroSection from './components/HeroSection.vue';
import SearchSection from './components/SearchSection.vue';
import ProductGrid from './components/ProductGrid.vue';
import TheFooter from './components/TheFooter.vue';
import Cart from './components/Cart.vue';
import ProductDetails from './components/ProductDetails.vue';

interface Product {
  id: number;
  title: string;
  image: string;
  price: number;
  category: string;
  quantity?: number;
}

interface Filter {
  priceMin?: number;
  priceMax?: number;
  categories?: {
    [key: string]: boolean;
  };
}

// Estado
const cartItems = ref<Product[]>([]);
const showCart = ref(false);
const searchQuery = ref('');
const activeFilters = ref<Filter>({});
const darkMode = ref(false);
const selectedProduct = ref<Product | null>(null);

// Carrito de compras
const addToCart = (product: Product) => {
  const existingItem = cartItems.value.find(item => item.id === product.id);
  if (existingItem) {
    existingItem.quantity = (existingItem.quantity || 0) + 1;
  } else {
    cartItems.value.push({...product, quantity: 1});
  }
  // Mostrar el carrito brevemente
  showCart.value = true;
  setTimeout(() => {
    if (!document.querySelector('.cart-container:hover')) {
      showCart.value = false;
    }
  }, 3000);
};

const removeFromCart = (productId: number) => {
  cartItems.value = cartItems.value.filter(item => item.id !== productId);
};

const updateQuantity = (productId: number, quantity: number) => {
  const item = cartItems.value.find(item => item.id === productId);
  if (item) {
    item.quantity = quantity;
  }
};

const checkout = () => {
  alert(`Compra finalizada. Total: ${cartTotal.value}€`);
  cartItems.value = [];
  showCart.value = false;
};

const cartTotal = computed(() => {
  return cartItems.value.reduce((total, item) => total + (item.price * (item.quantity || 0)), 0).toFixed(2);
});

const cartCount = computed(() => {
  return cartItems.value.reduce((count, item) => count + (item.quantity || 0), 0);
});

// Búsqueda y filtros
const handleSearch = (query: string) => {
  searchQuery.value = query;
};

const handleFilter = (filters: Filter) => {
  activeFilters.value = filters;
};

// Modo oscuro
const toggleDarkMode = () => {
  darkMode.value = !darkMode.value;
  if (darkMode.value) {
    document.documentElement.classList.add('dark');
  } else {
    document.documentElement.classList.remove('dark');
  }
};

// Detalles del producto
const viewProductDetails = (product: Product) => {
  selectedProduct.value = product;
};

// Inicializar modo oscuro según preferencia del sistema
onMounted(() => {
  if (window.matchMedia && window.matchMedia('(prefers-color-scheme: dark)').matches) {
    darkMode.value = true;
    document.documentElement.classList.add('dark');
  }
});
</script>