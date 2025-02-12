<template>
  <div class="flex flex-col items-center w-full gap-3">
    <input
      type="number"
      min="1"
      v-model.number="removeAmount"
      class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-red-500 text-gray-700"
    />
    <button
      @click="removeItem"
      class="bg-red-600 text-white font-semibold px-4 py-2 rounded-lg hover:bg-red-700 transition-all ease-in-out duration-300 w-full text-sm sm:text-xl md:text-3xl"
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
