<template>
  <div class="max-w-3xl mx-auto p-6 bg-white shadow-lg rounded-lg">
    <h1 class="text-2xl font-bold text-gray-800 border-b pb-2 mb-4">🛒 Your Cart</h1>

    <div v-if="items.length > 0">
      <div
        v-for="item in currentItems.items"
        :key="item.name"
        class="flex justify-between items-center bg-gray-100 p-4 mb-2 rounded-lg shadow-sm"
      >
        <div>
          <h2 class="text-lg font-semibold text-gray-700">{{ item.name }}</h2>
          <p class="text-sm text-gray-500">Price: ${{ item.price.toFixed(2) }}</p>
        </div>
        <span class="text-blue-600 font-semibold">x{{ item.quantity }}</span>
      </div>
      <h3>Total Cost: ${{ currentItems.totalCost.toFixed(2) }}</h3>
    </div>

    <p v-else class="text-gray-500 text-center">Your cart is empty.</p>
  </div>
</template>

<script setup>
defineProps({
  currentItems: {
    type: Object,
    required: true,
  },
})
</script>

<style scoped></style>
