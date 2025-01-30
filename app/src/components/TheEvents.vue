<template>
  <div>
    <p>{{ events[Math.floor(Math.random() * events.length)] }}</p>
  </div>
</template>

<script setup>
import { ref } from 'vue'
let events = ref([
  'You got something.',
  'Uh oh. You might have lost an item.',
  'You lost something, but found it again.',
])
</script>

<style scoped></style>
