<template>
  <!-- 🛒 Cart Container -->
  <div
    class="fixed flex-col top-[11%] bottom-[20%] right-0 overflow-y-auto w-1/3 mx-auto p-8 bg-white shadow-lg rounded-lg mt-10"
  >
    <!-- Cart Title (Larger font size) -->
    <h1
      class="w-full text-3xl sm:text-4xl font-extrabold text-gray-800 border-b pb-4 mb-8 text-center"
    >
      🛒 Your Cart
    </h1>

    <div v-if="items.length > 0">
      <div
        v-for="item in items"
        :key="item.name"
        class="flex flex-col items-center bg-gray-50 p-6 mb-6 rounded-xl shadow-md transition-all hover:shadow-xl text-center"
      >
        <div class="w-full">
          <!-- Item Name and Quantity (Aligned Side by Side) -->
          <div class="flex items-center justify-center gap-2 w-full">
            <h2 class="font-semibold text-gray-700 text-xl sm:text-2xl md:text-3xl text-center">
              {{ item.name }}
            </h2>
            <span class="text-lg sm:text-xl md:text-2xl text-gray-600 font-semibold">
              x{{ item.quantity }}
            </span>
          </div>

          <!-- Item Price (Centered) -->
          <p class="text-base sm:text-lg md:text-xl text-gray-500 text-center">
            Price: ${{ item.price.toFixed(2) }}
          </p>

          <!-- Total Cost of Item (Centered) -->
          <p class="text-sm sm:text-base md:text-lg text-gray-400 text-center">
            Total Cost of {{ item.name }}: ${{ item.totalPrice.toFixed(2) }}
          </p>

          <div class="flex justify-center items-center gap-4 mt-4">
            <RemoveButtonItems :itemId="item.name" @remove-item="removeFromCart" />
          </div>
        </div>
      </div>
    </div>

    <!-- Empty Cart Message -->
    <p v-else class="text-gray-500 text-center text-lg sm:text-xl md:text-2xl">
      Your cart is empty.
    </p>
  </div>

  <!-- 📌 Total Cost Box -->
  <div
    v-if="items.length > 0"
    class="fixed bottom-[5%] right-[0%] top-[85%] left-[70%] text-right p-8 bg-white shadow-lg rounded-lg z-10 w-[30%]"
  >
    <!-- Total Cost Header -->
    <h3
      class="w-full font-semibold text-gray-800 text-center text-sm sm:text-2xl md:text-2xl lg:text-xl"
    >
      Total Cost: ${{ totalCost.toFixed(2) }}
    </h3>
  </div>
</template>

<script setup>
import RemoveButtonItems from './RemoveButtonItems.vue'
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

function removeFromCart(id, removeAmount) {
  console.log('remove-item', id, removeAmount)
  emit('remove-item', id, removeAmount) // Pass the event to TheItems.vue
}
</script>

<style scoped></style>
