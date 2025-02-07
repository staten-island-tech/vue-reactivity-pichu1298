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
      <ShoppingCart
        :items="currentItems.items"
        :totalCost="currentItems.totalCost"
        @remove-item="removeItemFromCart"
      />
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import { reactive } from 'vue'
import ShoppingCart from './ShoppingCart.vue'
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
function removeItemFromCart(id, removeAmount) {
  console.log('Removing item with ID:', id, 'Amount to remove:', removeAmount)

  // Find the item in the cart
  const itemIndex = currentItems.items.findIndex((cartItem) => cartItem.name === id)

  // If item exists in the cart
  if (itemIndex !== -1) {
    let item = currentItems.items[itemIndex]

    // Check if removeAmount is greater than or equal to current quantity
    if (removeAmount >= item.quantity) {
      // Remove item completely
      currentItems.items.splice(itemIndex, 1)
    } else {
      // Decrease the quantity
      item.quantity -= removeAmount
      item.totalPrice = item.price * item.quantity
    }

    // Recalculate total cost
    currentItems.totalCost = currentItems.items.reduce(
      (total, item) => total + item.price * item.quantity,
      0,
    )
  }
}

const shoppingItems = ref([
  {
    name: 'Apples',
    description: 'Fresh and juicy red apples, perfect for snacking or baking.',
    imageUrl:
      'https://th.bing.com/th/id/R.bd0e8f356385ca315c2c53b49af90674?rik=mUGVWUPH95nt7g&riu=http%3a%2f%2ffillyourplate.org%2fblog%2fwp-content%2fuploads%2f2014%2f08%2fbigstock-Ripe-apples-on-the-tree-51573631.jpg&ehk=NLx1c4MBbuTFkvAmKT1r%2bsqHQ13aERlp3vboi9ruHqI%3d&risl=&pid=ImgRaw&r=0',
    price: 2.99,
    quantity: 1,
  },
  {
    name: 'Milk',
    description: 'A carton of fresh whole milk, great for cereal or coffee.',
    imageUrl: 'https://unblast.com/wp-content/uploads/2020/06/Milk-Carton-Packaging-Mockup.jpg',
    price: 3.49,
    quantity: 1,
  },
  {
    name: 'Bread',
    description: 'Soft and fluffy whole wheat bread, ideal for sandwiches.',
    imageUrl:
      'https://th.bing.com/th/id/R.92f8ee7be77d7b53d5304093b3861e18?rik=VJ9Fr5q6neawOQ&riu=http%3a%2f%2fupload.wikimedia.org%2fwikipedia%2fcommons%2f7%2f71%2fAnadama_bread_(1).jpg&ehk=8o8tB4WgouX4ktS06icsn57N2DKLcg95T9oUA%2b%2fSmQs%3d&risl=1&pid=ImgRaw&r=0',
    price: 2.79,
    quantity: 1,
  },
  {
    name: 'Eggs',
    description: 'A dozen organic eggs, rich in protein and essential nutrients.',
    imageUrl:
      'https://th.bing.com/th/id/R.ee0dd53830acf4ea8b06f11f9b1f7bba?rik=hVknUJjZAz0e3g&riu=http%3a%2f%2fphotos.demandstudios.com%2fgetty%2farticle%2f142%2f105%2f87532189.jpg&ehk=0dzGltL6%2f9gfKbRP90EC2YfHlQbzL69QCRqwydVK8S4%3d&risl=1&pid=ImgRaw&r=0',
    price: 4.99,
    quantity: 1,
  },
  {
    name: 'Chicken Breast',
    description: 'Skinless, boneless chicken breast, perfect for grilling or baking.',
    imageUrl:
      'https://1.bp.blogspot.com/-8QTDNCNvXt4/XwsHvghqZ_I/AAAAAAAABDQ/LYt253LT098trcneNlQx5XL9DS-LWmC9ACLcBGAsYHQ/s1800/Oven-Baked-Chicken-Breasts-IMAGE-37.jpg',
    price: 6.99,
    quantity: 1,
  },
  {
    name: 'Rice',
    description: 'Long-grain white rice, a versatile staple for many dishes.',
    imageUrl: 'https://cdn.loveandlemons.com/wp-content/uploads/2020/03/how-to-cook-rice.jpg',
    price: 5.49,
    quantity: 1,
  },
  {
    name: 'Toothpaste',
    description: 'Mint-flavored toothpaste for fresh breath and strong teeth.',
    imageUrl:
      'https://i5.walmartimages.com/asr/bcdc51fa-cc5a-4269-8b9d-d4a056cd0125_1.bcbe1032851dc7259967c13505ba50d6.jpeg',
    price: 3.99,
    quantity: 1,
  },
  {
    name: 'Shampoo',
    description: 'Nourishing shampoo that keeps hair soft and healthy.',
    imageUrl:
      'https://i5.walmartimages.com/asr/6518ee99-5914-4788-850b-dd74a760f4af.585ee92a94d078307efdbab8a80ad769.jpeg',
    price: 7.29,
    quantity: 1,
  },
  {
    name: 'Laundry Detergent',
    description: 'Powerful liquid detergent for clean and fresh-smelling clothes.',
    imageUrl:
      'https://www.thespruce.com/thmb/pmfCoOzxFR7anVPz7zzpHlp0N3E=/3000x3000/filters:no_upscale():max_bytes(150000):strip_icc()/gainlaundrydetergent-465c56fd9cb64b98938c953f9aa1371c.jpeg',
    price: 10.99,
    quantity: 1,
  },
  {
    name: 'Coffee',
    description: 'Rich and aromatic ground coffee, perfect for your morning brew.',
    imageUrl:
      'https://th.bing.com/th/id/R.ee280908b6bfabb36b2331ca9bc74bba?rik=LWYtJCdXRGgD7w&riu=http%3a%2f%2fupload.wikimedia.org%2fwikipedia%2fcommons%2f0%2f0c%2fCoffee_time_(2410222127).jpg&ehk=02vR0%2f4hvYSxrYpiplY8EkDo49xkRLDplmKFADkjgZc%3d&risl=&pid=ImgRaw&r=0',
    price: 8.99,
    quantity: 1,
  },
  {
    name: 'Cereal',
    description: 'Crunchy and delicious breakfast cereal with whole grains.',
    imageUrl:
      'https://i5.walmartimages.com/asr/e3597292-a7ba-429e-ac27-0f91c80e916b.ac0621fbeca841ba772e993a5721229f.jpeg',
    price: 4.59,
    quantity: 1,
  },
  {
    name: 'Cheese',
    description: 'A block of sharp cheddar cheese, great for sandwiches or snacks.',
    imageUrl:
      'https://th.bing.com/th/id/R.ad02987b2d8e8a1dd265ce8c95e54292?rik=fzco4RMvxKotWA&riu=http%3a%2f%2fdeliciousfoodandwine.com%2fwp-content%2fuploads%2f2015%2f03%2fDollarphotoclub_53674521.jpg&ehk=awS5zy%2bK64%2fPQsQldskF7Cp3Ksatb0UpybU1elwlpXU%3d&risl=&pid=ImgRaw&r=0',
    price: 5.79,
    quantity: 1,
  },
])
</script>

<style scoped></style>
