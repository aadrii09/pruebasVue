<template>
  <header class="w-full py-4 px-6 flex items-center justify-between text-white dark:bg-gray-900">
    <nav class="flex items-center space-x-8">
      <a href="#" class="text-xl font-bold">Marcas</a>
      <a href="#" class="text-xl font-bold">Productos</a>
    </nav>
    
    <div class="flex-shrink-0">
      <div class="text-2xl font-bold text-center">PixelVault</div>
    </div>
    
    <div class="flex items-center space-x-8">
      <button @click="$emit('toggle-cart')" class="text-xl font-bold relative">
        Carrito
        <span v-if="cartCount > 0" class="absolute -top-2 -right-2 bg-accent text-white text-xs rounded-full w-5 h-5 flex items-center justify-center cart-animation">
          {{ cartCount }}
        </span>
      </button>
      <a href="#" class="text-xl font-bold">Perfil</a>
    </div>
  </header>
</template>

<script setup lang="ts">
defineProps({
  cartCount: {
    type: Number,
    default: 0
  }
});

defineEmits(['toggle-cart']);
</script>