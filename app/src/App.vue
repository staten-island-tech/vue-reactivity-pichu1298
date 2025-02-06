<script setup>
import { RouterView } from 'vue-router'
</script>

<template>
  <div class="flex flex-col items-center justify-center min-h-screen bg-gray-50 py-12">
    <h1 class="text-4xl font-extrabold text-gray-900 mb-8">Store</h1>
    <RouterView />
  </div>
</template>

<style scoped></style>
