<template>
  <div class="flex items-center gap-3 space-x-3 w-full">
    <input
      type="number"
      min="1"
      v-model.number="removeAmount"
      class="w-16 sm:w-20 px-3 py-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-red-500 text-gray-700"
    />
    <button
      @click="removeItem"
      class="bg-red-600 text-white font-semibold px-4 py-2 rounded-lg hover:bg-red-700 transition-all ease-in-out duration-300"
    >
      Remove
    </button>
  </div>
</template>

<script setup>
import { defineProps, defineEmits, ref } from 'vue'

let props = defineProps({
  itemId: String, // Receives the item's ID
})
const removeAmount = ref(1)
let emit = defineEmits(['remove-item']) // Sends event to ShoppingCart.vue

function removeItem() {
  console.log('remove-item', props.itemId, removeAmount.value)
  emit('remove-item', props.itemId, removeAmount.value) // Sends itemId to the parent (ShoppingCart.vue)
}
</script>
