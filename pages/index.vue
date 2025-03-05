<template>
    <div class="min-h-screen bg-gradient-to-br from-blue-100 to-purple-100 flex flex-col items-center justify-center text-gray-900 p-6">
      <main class="text-center max-w-3xl w-full px-8">
     
        <!-- Animated Heading -->
        <h1 class="text-5xl md:text-6xl font-extrabold text-gray-800 animate-fade-in-up">
          Test Your Knowledge!
        </h1>
  
        <!-- Animated Subheading -->
        <p class="text-lg md:text-xl text-gray-700 mt-4 mb-8 leading-relaxed animate-fade-in-up delay-100">
          Explore a variety of quizzes and challenge yourself with fun and engaging questions.
        </p>
  
        <!-- Animated Button -->
        <NuxtLink
          to="/quiz"
          class="px-10 py-5 bg-gradient-to-r from-blue-500 to-purple-600 text-white font-semibold rounded-full shadow-md hover:shadow-lg transition-all duration-300 transform hover:scale-105 hover:ring-4 hover:ring-purple-300 animate-fade-in-up delay-200"
        >
          Start Quiz
        </NuxtLink>
  
    
      </main>
    </div>
  </template>
  
  <style>
  @keyframes fade-in-up {
    0% {
      opacity: 0;
      transform: translateY(20px);
    }
    100% {
      opacity: 1;
      transform: translateY(0);
    }
  }
  
  .animate-fade-in-up {
    animation: fade-in-up 0.8s ease-out forwards;
  }
  
  .delay-100 {
    animation-delay: 0.1s;
  }
  
  .delay-200 {
    animation-delay: 0.2s;
  }
  
  .delay-300 {
    animation-delay: 0.3s;
  }
  </style>
  