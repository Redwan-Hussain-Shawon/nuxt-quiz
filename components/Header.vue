<template>
    <header class="bg-white shadow-md">
    <div class="container mx-auto flex justify-between items-center py-4 px-6">
      <!-- Logo & Text -->
      <div class="flex items-center space-x-3">
        <span class="text-xl font-bold text-gray-800">My Website</span>
      </div>
  
      <!-- Navigation Links -->
      <nav class="hidden md:flex space-x-6">
        <a href="#" class="text-gray-600 hover:text-blue-500">Home</a>
        <a href="#" class="text-gray-600 hover:text-blue-500">About</a>
        <a href="#" class="text-gray-600 hover:text-blue-500">Dashboard</a>
      </nav>
  
      <!-- Login/Register Buttons -->
      <div class="space-x-4">

        <NuxtLink to="/auth/login" class="bg-blue-600 text-white px-4 py-2 rounded hover:bg-blue-700">Login</NuxtLink>
        <NuxtLink to="#" class="bg-blue-600 text-white px-4 py-2 rounded hover:bg-blue-700">Register</NuxtLink>
      </div>
    </div>
  </header>
  
</template>