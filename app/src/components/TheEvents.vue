<template>
  <div>
    <p>Hi</p>
  </div>
</template>

<script setup>
import { reactive } from 'vue'
let events = reactive({
  goodLuck: 'You got something.',
  badLuck: 'Uh oh. You might have lost an item.',
  confusingLuck: 'You lost something, but found it again.',
})
</script>

<style scoped></style>
