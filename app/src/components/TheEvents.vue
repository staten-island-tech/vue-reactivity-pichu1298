<template>
  <div>
    <p>{{ randomEvent }}</p>
  </div>
</template>

<script setup>
import { ref } from 'vue'
let events = ref([
  'You got something.',
  'Uh oh. You might have lost an item.',
  'You lost something, but found it again.',
])
let randomEvent = events[Math.floor(Math.random() * events.length)]
defineProps({
  count: Number,
})
function checkCount() {
  if (count >= 5) {
    count = 0
    randomEvent = events[Math.floor(Math.random() * events.length)]
  }
}
</script>

<style scoped></style>
