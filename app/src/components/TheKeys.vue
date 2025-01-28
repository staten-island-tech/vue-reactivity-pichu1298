<template>
  <div>
    <h1>Your current coordinates are ({{ xValue }} , {{ yValue }}).</h1>
    <button class="btn" @click="XLocationLeft">Move Left</button>
    <button class="btn" @click="XLocationRight">Move Right</button>
    <button class="btn" @click="YLocationUp">Move Up</button>
    <button class="btn" @click="YLocationDown">Move Down</button>
  </div>
</template>

<script setup>
import { ref } from 'vue'

let xValue = ref(0)
let yValue = ref(0)
function XLocationLeft() {
  xValue.value--
}
function XLocationRight() {
  xValue.value++
}
function YLocationUp() {
  yValue.value++
}
function YLocationDown() {
  yValue.value--
}

//scoped fixes CssStyleConfllicts.
//ref is ... something for counting..?
</script>

<style scoped></style>
