<template>
  <div>
    <button @click="checkedOut">Check Out</button>
  </div>
</template>

<script setup>
import { emit } from 'vue'
let emit = defineEmits(['check-out'])
function checkedOut() {
  emit('check-out')
}
</script>

<style scoped></style>
