<template>
  <div>
    <input type="number" placeholder="amount" v-model="amount" />
    <button type="submit" @click="RemoveItem(amount, item.id)">Remove</button>
  </div>
</template>

<script setup>
import { defineProps, defineEmits } from 'vue'

let cart = defineProps({
  items: {
    type: Array,
    required: true,
  },
  totalCost: {
    type: Number,
    required: true,
  },
})
function RemoveItem(amount, item) {}
</script>

<style scoped></style>
