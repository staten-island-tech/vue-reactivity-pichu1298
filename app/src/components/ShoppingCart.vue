<template>
  <div>
    <h1>Your Cart</h1>
    <div v-for="item in items" :key="item.name">
      <h2>{{ item.name }}</h2>
      <h2>{{ item.price }}</h2>
    </div>
  </div>
</template>

<script setup>
defineProps({
  items: Array,
})
</script>

<style scoped></style>
