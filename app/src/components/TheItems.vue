<template>
  <div class="flex justify-between p-6">
    <!-- Shopping Items (Left Side - 2/3 width) -->
    <div class="w-2/3 pr-6">
      <div class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 gap-6">
        <div
          v-for="item in shoppingItems"
          :key="item.name"
          class="bg-white shadow-lg rounded-2xl p-4 transition-transform transform hover:scale-105 border border-gray-200"
        >
          <h1 class="text-xl font-bold text-gray-800">{{ item.name }}</h1>
          <img :src="item.imageUrl" alt="" class="w-full h-48 object-cover rounded-lg mt-2" />
          <p class="text-gray-600 mt-2">{{ item.description }}</p>

          <div class="mt-4 flex flex-col gap-3">
            <input
              v-model.number="item.quantity"
              type="number"
              min="1"
              placeholder="Enter quantity"
              class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-400"
            />
            <button
              @click="addToCart(item)"
              type="submit"
              class="bg-blue-600 text-white font-semibold py-2 px-4 rounded-lg hover:bg-blue-700 transition-all"
            >
              Add to Cart (${{ (item.price * (item.quantity || 1)).toFixed(2) }})
            </button>
          </div>
        </div>
      </div>
    </div>

    <!-- Shopping Cart (Right Side - 1/3 width) -->
    <div class="w-1/3 bg-gray-50 p-4 border-l border-gray-300 rounded-lg">
      <ShoppingCart :items="currentItems.items" :totalCost="currentItems.totalCost" />
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import { reactive } from 'vue'
import ShoppingCart from './ShoppingCart.vue'
import RemoveButtonItems from './RemoveButtonItems.vue'
let currentItems = reactive({ items: [], totalCost: 0 })
function addToCart(item) {
  const existingItem = currentItems.items.find((cartItem) => cartItem.name === item.name)

  if (!existingItem) {
    currentItems.items.push({
      name: item.name,
      price: item.price,
      totalPrice: item.price * item.quantity,
      quantity: item.quantity,
    })
  } else {
    existingItem.quantity += item.quantity
    existingItem.totalPrice += item.quantity * item.price
  }
  currentItems.totalCost = currentItems.items.reduce(
    (total, item) => total + item.price * item.quantity,
    0,
  )

  console.log(currentItems)
}

const shoppingItems = ref([
  {
    name: 'Apples',
    description: 'Fresh and juicy red apples, perfect for snacking or baking.',
    imageUrl: '',
    price: 2.99,
    quantity: 1,
  },
  {
    name: 'Milk',
    description: 'A carton of fresh whole milk, great for cereal or coffee.',
    imageUrl: '',
    price: 3.49,
    quantity: 1,
  },
  {
    name: 'Bread',
    description: 'Soft and fluffy whole wheat bread, ideal for sandwiches.',
    imageUrl: '',
    price: 2.79,
    quantity: 1,
  },
  {
    name: 'Eggs',
    description: 'A dozen organic eggs, rich in protein and essential nutrients.',
    imageUrl: '',
    price: 4.99,
    quantity: 1,
  },
  {
    name: 'Chicken Breast',
    description: 'Skinless, boneless chicken breast, perfect for grilling or baking.',
    imageUrl: '',
    price: 6.99,
    quantity: 1,
  },
  {
    name: 'Rice',
    description: 'Long-grain white rice, a versatile staple for many dishes.',
    imageUrl: '',
    price: 5.49,
    quantity: 1,
  },
  {
    name: 'Toothpaste',
    description: 'Mint-flavored toothpaste for fresh breath and strong teeth.',
    imageUrl: '',
    price: 3.99,
    quantity: 1,
  },
  {
    name: 'Shampoo',
    description: 'Nourishing shampoo that keeps hair soft and healthy.',
    imageUrl: '',
    price: 7.29,
    quantity: 1,
  },
  {
    name: 'Laundry Detergent',
    description: 'Powerful liquid detergent for clean and fresh-smelling clothes.',
    imageUrl: '',
    price: 10.99,
    quantity: 1,
  },
  {
    name: 'Coffee',
    description: 'Rich and aromatic ground coffee, perfect for your morning brew.',
    imageUrl: '',
    price: 8.99,
    quantity: 1,
  },
  {
    name: 'Cereal',
    description: 'Crunchy and delicious breakfast cereal with whole grains.',
    imageUrl: '',
    price: 4.59,
    quantity: 1,
  },
  {
    name: 'Cheese',
    description: 'A block of sharp cheddar cheese, great for sandwiches or snacks.',
    imageUrl: '',
    price: 5.79,
    quantity: 1,
  },
])
</script>

<style scoped></style>
