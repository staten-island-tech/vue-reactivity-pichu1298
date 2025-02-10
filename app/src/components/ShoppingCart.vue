<template>
  <div
    class="fixed flex-col top-20 bottom-20 right-0 overflow-y-auto w-1/3 mx-auto p-8 bg-white shadow-lg rounded-lg mt-10"
  >
    <h1 class="w-full text-4xl font-extrabold text-gray-800 border-b pb-4 mb-8 text-center">
      🛒 Your Cart
    </h1>

    <div v-if="items.length > 0">
      <div
        v-for="item in items"
        :key="item.name"
        class="flex flex-col sm:flex-row justify-between items-center bg-gray-50 p-6 mb-6 rounded-xl shadow-md transition-all hover:shadow-xl"
      >
        <div class="flex-1">
          <h2 class="text-2xl font-semibold text-gray-700">{{ item.name }}</h2>
          <p class="text-base text-gray-500">Price: ${{ item.price.toFixed(2) }}</p>
          <p class="text-sm text-gray-400">
            Total Cost of {{ item.name }}: ${{ item.totalPrice.toFixed(2) }}
          </p>
        </div>

        <div class="flex items-center space-x-6 mt-4 sm:mt-0">
          <span class="text-xl text-gray-600 font-semibold">x{{ item.quantity }}</span>
          <RemoveButtonItems :itemId="item.name" @remove-item="removeFromCart" />
        </div>
      </div>
    </div>
    <p v-else class="text-gray-500 text-center text-lg">Your cart is empty.</p>
  </div>
  <div
    v-if="items.length > 0"
    class="fixed bottom-10 right-10 text-right p-8 bg-white shadow-lg rounded-lg z-10"
  >
    <h3 class="text-2xl font-semibold text-gray-800">Total Cost: ${{ totalCost.toFixed(2) }}</h3>
  </div>
</template>

<script setup>
import RemoveButtonItems from './RemoveButtonItems.vue'
import CheckOut from './CheckOut.vue'
const props = defineProps({
  items: {
    type: Array,
    required: true,
  },
  totalCost: {
    type: Number,
    required: true,
  },
})

const emit = defineEmits(['remove-item']) // Sends event up to TheItems.vue

function checkOut() {
  emit('check-out')
}

function removeFromCart(id, removeAmount) {
  console.log('remove-item', id, removeAmount)
  emit('remove-item', id, removeAmount) // Pass the event to TheItems.vue
}
</script>

<style scoped></style>
