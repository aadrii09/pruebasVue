<template>
  <header class="w-full py-4 px-6 bg-[#1f2034] text-white">
    <div class="container mx-auto flex items-center justify-between">
      <div class="flex items-center">
        <span class="ml-3 text-xl font-bold">PixelVault</span>
      </div>
      <nav class="hidden md:block">
        <ul class="flex space-x-8">
          <li><a href="#" class="hover:text-gray-300">Marcas</a></li>
          <li><a href="#" class="hover:text-gray-300">Productos</a></li>
          <li><a href="#" class="hover:text-gray-300">Perfil</a></li>
          <li><a href="#" class="hover:text-gray-300">Carrito</a></li>
        </ul>
      </nav>
      <button class="md:hidden text-white">
        <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none"
             viewBox="0 0 24 24" stroke="currentColor">
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                d="M4 6h16M4 12h16M4 18h16"/>
        </svg>
      </button>
    </div>
  </header>
</template>