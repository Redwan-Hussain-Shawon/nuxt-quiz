<template>
    <div class="min-h-screen bg-gray-100 flex flex-col items-center py-12 px-6">
      <h1 class="text-4xl font-extrabold text-gray-800 mb-10">Choose a Quiz Category</h1>
  
      <div class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4 gap-6 w-full max-w-6xl">
        <NuxtLink 
          v-for="category in categories" 
          :key="category.id" 
          :to="`/quiz/${category.id}`" 
          class="group relative bg-white rounded-xl shadow-lg hover:shadow-2xl p-6 flex flex-col items-center justify-center text-center transition-transform transform hover:-translate-y-2 hover:scale-105"
          :style="{ background: category.bg }"
        >
          <div class="text-5xl text-white">
            <i :class="category.icon"></i>
          </div>
          <h2 class="text-xl font-bold text-white mt-4">{{ category.name }}</h2>
          <div class="absolute inset-0 bg-black bg-opacity-20 rounded-xl opacity-0 group-hover:opacity-50 transition-opacity"></div>
        </NuxtLink>
      </div>
    </div>
  </template>
  
  <script setup>
  import { ref } from 'vue';
  const categories = reactive([
  { name: "Entertainment: Books", id: "10", icon: "fas fa-book", bg: "linear-gradient(135deg, #8e44ad, #3498db)" },
  { name: "Entertainment: Film", id: "11", icon: "fas fa-film", bg: "linear-gradient(135deg, #e74c3c, #f1c40f)" },
  { name: "Entertainment: Music", id: "12", icon: "fas fa-music", bg: "linear-gradient(135deg, #9b59b6, #e74c3c)" },
  { name: "Entertainment: Musicals & Theatres", id: "13", icon: "fas fa-theater-masks", bg: "linear-gradient(135deg, #d35400, #f39c12)" },
  { name: "Entertainment: Television", id: "14", icon: "fas fa-tv", bg: "linear-gradient(135deg, #c0392b, #8e44ad)" },
  { name: "Entertainment: Video Games", id: "15", icon: "fas fa-gamepad", bg: "linear-gradient(135deg, #27ae60, #2980b9)" },
  { name: "Entertainment: Board Games", id: "16", icon: "fas fa-chess", bg: "linear-gradient(135deg, #16a085, #2c3e50)" },
  { name: "Science & Nature", id: "17", icon: "fas fa-leaf", bg: "linear-gradient(135deg, #1abc9c, #27ae60)" },
  { name: "Science: Computers", id: "18", icon: "fas fa-laptop", bg: "linear-gradient(135deg, #2980b9, #3498db)" },
  { name: "Science: Mathematics", id: "19", icon: "fas fa-square-root-alt", bg: "linear-gradient(135deg, #e67e22, #e74c3c)" },
  { name: "Mythology", id: "20", icon: "fas fa-dragon", bg: "linear-gradient(135deg, #c0392b, #8e44ad)" },
  { name: "Sports", id: "21", icon: "fas fa-basketball-ball", bg: "linear-gradient(135deg, #e74c3c, #f39c12)" },
  { name: "Geography", id: "22", icon: "fas fa-globe", bg: "linear-gradient(135deg, #2ecc71, #3498db)" },
  { name: "History", id: "23", icon: "fas fa-history", bg: "linear-gradient(135deg, #f1c40f, #e67e22)" },
  { name: "Politics", id: "24", icon: "fas fa-gavel", bg: "linear-gradient(135deg, #34495e, #7f8c8d)" },
  { name: "Art", id: "25", icon: "fas fa-paint-brush", bg: "linear-gradient(135deg, #e74c3c, #9b59b6)" },
  { name: "Celebrities", id: "26", icon: "fas fa-star", bg: "linear-gradient(135deg, #f1c40f, #e67e22)" },
  { name: "Animals", id: "27", icon: "fas fa-paw", bg: "linear-gradient(135deg, #e67e22, #d35400)" },
  { name: "Vehicles", id: "28", icon: "fas fa-car", bg: "linear-gradient(135deg, #e74c3c, #c0392b)" },
  { name: "Entertainment: Comics", id: "29", icon: "fas fa-book-open", bg: "linear-gradient(135deg, #3498db, #2980b9)" },
  { name: "Science: Gadgets", id: "30", icon: "fas fa-cogs", bg: "linear-gradient(135deg, #2c3e50, #34495e)" },
  { name: "Entertainment: Japanese Anime & Manga", id: "31", icon: "fas fa-tv", bg: "linear-gradient(135deg, #e74c3c, #8e44ad)" },
  { name: "Entertainment: Cartoon & Animations", id: "32", icon: "fas fa-film", bg: "linear-gradient(135deg, #1abc9c, #16a085)" }
]);

  </script>
  
  <style>
  @import url('https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css');
  </style>
  