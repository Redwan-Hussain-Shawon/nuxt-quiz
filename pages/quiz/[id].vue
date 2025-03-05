<template>
  <div v-if="questions.length > 0 && isQuizStarted" class="min-h-screen bg-gradient-to-br from-blue-50 to-purple-50 py-12 px-6">
    <div class="max-w-4xl mx-auto">
      
    <!-- School and Student Info -->
<div class="text-center mb-12">
  <h1 class="text-5xl font-extrabold text-gray-900 mb-6 leading-tight">
    Welcome to the Quiz
  </h1>
  <div class="bg-gradient-to-r from-blue-500 to-purple-500 text-white rounded-lg py-4 px-6 max-w-lg mx-auto shadow-lg">
    <p class="text-xl font-medium mb-2">School: <span class="font-semibold text-yellow-300">Dumy School of Excellence</span></p>
    <p class="text-lg font-medium mb-2">Student: <span class="font-semibold text-yellow-300">Redwan Hussain Shawon</span></p>
    <p class="text-lg font-medium">Class: <span class="font-semibold text-yellow-300">12th Grade - Science</span></p>
  </div>
</div>
<div v-if="!quizFinished">
      <div class="mb-6">
        <div class="text-center mb-4 text-lg font-semibold text-gray-700">
          Questions
        </div>
        <div class="grid grid-cols-6 gap-4">
          <button 
            v-for="(question, index) in questions" 
            :key="index" 
            @click="goToQuestion(index)"
            :class="{
              'bg-blue-500 text-white': currentIndex === index,  
              'bg-white text-gray-800': currentIndex !== index
            }"
            class="w-12 h-12 flex justify-center items-center rounded-full border-2 shadow-lg hover:shadow-2xl transition-all duration-300 transform hover:scale-110 cursor-pointer"
          >
            {{ index + 1 }}
          </button>
        </div>
      </div>

      <!-- Progress Bar -->
      <div class="mb-6">
        <div class="text-sm text-gray-600 text-center">
          Question {{ currentIndex + 1 }} of {{ questions.length }}
        </div>
        <div class="w-full bg-gray-300 rounded-full h-3 mt-2">
          <div class="bg-blue-600 h-3 rounded-full transition-all duration-500" 
               :style="{ width: `${((currentIndex + 1) / questions.length) * 100}%` }">
          </div>
        </div>
      </div>

      <!-- Time Left -->
      <div class="mb-6 text-center text-lg font-semibold text-gray-700">
        Time Left: {{ formatTime(timeLeft) }}
      </div>

      <!-- Question Card -->
      <div class="bg-white p-6 rounded-xl shadow-xl border-t-4 border-blue-500 transition-all duration-300">
        <h2 v-if="questions[currentIndex]" class="text-xl font-semibold text-gray-800 mb-4 leading-snug">
          {{ currentIndex + 1 }}) {{ decodeHtml(questions[currentIndex].question) }}
        </h2>
        <div class="space-y-3">
          <label 
            v-for="(option, index) in shuffledOptions" 
            :key="index" 
            class="flex items-center space-x-3 p-4 rounded-lg border transition-all duration-200 cursor-pointer
                   hover:shadow-lg hover:bg-blue-50"
            :class="{ 'bg-blue-100 border-blue-500': selectedAnswer[currentIndex] === option }"
          >
            <input 
              type="radio" 
              :name="`question-${currentIndex}`" 
              :value="option" 
              v-model="selectedAnswer[currentIndex]" 
              class="hidden"
            >
            <span class="w-5 h-5 border border-gray-400 rounded-full flex items-center justify-center"
                  :class="{ 'bg-blue-500 border-blue-500': selectedAnswer[currentIndex] === option }">
              <span v-if="selectedAnswer[currentIndex] === option" class="w-2 h-2 bg-white rounded-full"></span>
            </span>
            <span class="text-gray-700">{{ decodeHtml(option) }}</span>
          </label>
        </div>
      </div>
    </div>
      <!-- Bottom Navigation -->
      <div class="fixed bottom-0 left-0 w-full bg-white shadow-lg py-3 flex justify-between items-center px-6">
        <button 
          @click="prevQuestion" 
          :disabled="currentIndex === 0"
          class="px-6 py-2 bg-gray-400 text-white rounded-lg hover:bg-gray-500 transition disabled:opacity-50"
        >
          Previous
        </button>

        <span class="text-gray-700 font-semibold"> {{ currentIndex + 1 }} / {{ questions.length }} </span>

        <button 
          @click="nextQuestion" 
          class="px-6 py-2 bg-blue-500 text-white rounded-lg hover:bg-blue-600 transition disabled:opacity-50"
        >
          Next
        </button>
      </div>

      <!-- Quiz Result -->
      <div v-if="quizFinished" class="bg-white p-8 rounded-xl shadow-lg mt-8 text-center">
        <h2 class="text-2xl font-semibold mb-4">Quiz Finished!</h2>
        <p class="text-lg">Your Score: <strong>{{ score }}</strong> / {{ questions.length }}</p>
        <p v-if="score >= questions.length / 2" class="text-green-600 mt-2">🎉 Great Job! You Passed!</p>
        <p v-else class="text-red-600 mt-2">😔 Better Luck Next Time!</p>
        <button @click="restartQuiz" 
                class="mt-4 bg-blue-500 text-white px-6 py-2 rounded-lg hover:bg-blue-600 transition">
          Restart Quiz
        </button>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed, onMounted } from 'vue';
import { useRoute } from 'vue-router';
import Swal from "sweetalert2";

const requestFullScreen = () => {
  const elem = document.documentElement;
  if (elem.requestFullscreen) {
    elem.requestFullscreen();
  }
};

const decodeHtml = (html) => {
  const txt = document.createElement("textarea");
  txt.innerHTML = html;
  return txt.value;
};

const route = useRoute();
const categoryId = route.params.id;
const questions = ref([]);
const currentIndex = ref(0);
const selectedAnswer = ref([]);
const isQuizStarted = ref(false);
const exitCount = ref(0);
const score = ref(0);
const quizFinished = ref(false);
const totalTime = ref(0); 
const timeLeft = ref(0); 
const timer = ref(null);

const startTimer = () => {
  if (questions.value.length > 0) {
    totalTime.value = questions.value.length * 60; // Assuming 1 minute per question
    timeLeft.value = totalTime.value;

    timer.value = setInterval(() => {
      if (timeLeft.value > 0) {
        timeLeft.value--; // Decrease timeLeft every second
      } else {
        finishQuiz()
      }
    }, 1000);
  }
};

const finishQuiz = () => {
  score.value = selectedAnswer.value.reduce((total, answer, index) => {
    const correctAnswer = decodeHtml(questions.value[index].correct_answer);
    return total + (answer === correctAnswer ? 1 : 0);
  }, 0);
  quizFinished.value = true;
};


const shuffledOptions = computed(() => {
  if (questions.value.length === 0) return [];
  const currentQuestion = questions.value[currentIndex.value];
  if (!currentQuestion) return [];
  const options = [
    decodeHtml(currentQuestion.correct_answer),
    ...currentQuestion.incorrect_answers.map(decodeHtml)
  ];
  return options.sort(() => Math.random() - 0.5);
});

const nextQuestion = () => {
  if (currentIndex.value < questions.value.length - 1) {
    currentIndex.value++;
  } else {
    score.value = selectedAnswer.value.reduce((total, answer, index) => {
      const correctAnswer = decodeHtml(questions.value[index].correct_answer);
      return total + (answer === correctAnswer ? 1 : 0);
    }, 0);
    quizFinished.value = true;
  }
};

const prevQuestion = () => {
  if (currentIndex.value > 0) {
    currentIndex.value--;
  }
};

const goToQuestion = (index) => {
  currentIndex.value = index;
};

const startQuiz = () => {
  Swal.fire({
    title: "Enter Fullscreen Mode",
    text: "The quiz will run in fullscreen mode for a better experience. Click 'Start' to begin.",
    icon: "info",
    confirmButtonText: "Start",
    allowOutsideClick: false,
    allowEscapeKey: false,
  }).then((result) => {
    if (result.isConfirmed) {
      requestFullScreen();
      isQuizStarted.value = true;
    }
  });
};

const checkFullscreen = () => {
  if (!document.fullscreenElement) {
    exitCount.value++;
    if (exitCount.value >= 2) {
      isQuizStarted.value = false;
      Swal.fire({
        title: "Quiz Canceled",
        text: "You have exited fullscreen twice. The quiz is canceled.",
        icon: "warning",
        confirmButtonText: "OK",
      }).then(() => {
        window.location = '/';
      });
    } else {
      startQuiz();
      isQuizStarted.value = false;
    }
  }
};

const restartQuiz = () => {
  window.location.reload();
};
const formatTime = (seconds) => {
  const minutes = Math.floor(seconds / 60);
  const remainingSeconds = seconds % 60;
  return `${minutes}:${remainingSeconds < 10 ? '0' : ''}${remainingSeconds}`;
};

onMounted(async () => {
  startQuiz();
 
  document.addEventListener("fullscreenchange", checkFullscreen);
  try {
    const response = await fetch(`https://opentdb.com/api.php?amount=10&category=${categoryId}&difficulty=medium&type=multiple`);
    const data = await response.json();
    questions.value = data.results;
    startTimer()
  } catch (err) {
    console.error("Failed to fetch data:", err);
  }
});
</script>
