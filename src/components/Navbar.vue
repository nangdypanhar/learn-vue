<script setup>
import logo from "@/assets/img/logo.jpg";
</script>

<template>
  <nav class="bg-green-700 border-b border-green-500">
    <div class="mx-auto max-w-7xl px-2 sm:px-6 lg:px-8">
      <div class="flex h-20 items-center justify-between">
        <div
          class="flex flex-1 items-center justify-center md:items-stretch md:justify-start"
        >
          <!-- Logo -->
          <img class="h-10 w-auto" :src="logo" alt="Vue Jobs" />
          <span class="hidden md:block text-white text-2xl font-bold ml-2"
            >Hello world</span
          >
          <div class="md:ml-auto">
            <div class="flex space-x-2"></div>
          </div>
        </div>
      </div>
    </div>
  </nav>
</template>
