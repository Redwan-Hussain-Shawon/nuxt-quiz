<script setup>
import Label from '@/components/Form/Label.vue';
import Input from '@/components/Form/Input.vue';

const form = reactive({
    email:null,
    password:null,
})

const handleSubmit=()=>{
    console.log(form)
}
</script>

<template>
    <div class="flex min-h-screen items-center justify-center bg-gray-100">
      <div class="bg-white shadow-lg rounded-lg p-8 w-full max-w-md">
        <h2 class="text-2xl font-bold text-center text-gray-800 mb-6">Login</h2>
  
        <form @submit.prevent="handleSubmit" method="POST">
          <!-- Email Input -->
          <div class="mb-4">
            <Label for="email"> Email </Label>
              <Input v-model="form.email" type="email" id="email" name="email" placeholder="Enter your email"  />
          </div>
  
          <!-- Password Input -->
          <div class="mb-4">
           <Label for="password"> Password </Label>
              <Input v-model="form.password" type="password" id="password" name="password" placeholder="Enter your password"  />
          </div>
  
          <!-- Login Button -->
          <button type="submit" 
            class="w-full bg-blue-500 text-white py-2 rounded-lg hover:bg-blue-600 transition">
            Login
          </button>
        </form>
  
        <!-- OR Separator -->
        <div class="flex items-center my-4">
          <div class="flex-1 h-px bg-gray-300"></div>
          <span class="px-3 text-gray-500">OR</span>
          <div class="flex-1 h-px bg-gray-300"></div>
        </div>
  
        <!-- Social Login Buttons -->
        <div class="flex gap-5">
          <button class="w-full flex items-center justify-center gap-2 bg-blue-600 text-white py-3 rounded-md hover:bg-blue-700 transition">
            <Icon name="uil:facebook" style="color: white"  />
          </button>
  
          <button class="w-full flex items-center justify-center gap-2 bg-red-500 text-white py-3 rounded-md hover:bg-red-600 transition ">
            <Icon name="mdi:google" style="color: white;" />
          </button>
  
          <button class="w-full flex items-center justify-center gap-2 bg-gray-800 text-white py-3 rounded-md hover:bg-gray-900 transition">
            <Icon name="uil:github" style="color: white" /> 
          </button>
        </div>
  
        <!-- Register & Forgot Password Links -->
        <div class="mt-4 text-center">
          <a href="#" class="text-blue-500 hover:underline">Forgot Password?</a>
        </div>
        <div class="mt-2 text-center">
          <p class="text-gray-600">Don't have an account? 
            <a href="#" class="text-blue-500 hover:underline">Register</a>
          </p>
        </div>
      </div>
    </div>
  </template>
  