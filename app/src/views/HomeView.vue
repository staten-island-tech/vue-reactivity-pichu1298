<template>
  <div>
    <TheKeys />
    <TheEvents />
  </div>
</template>

<script setup>
//scoped fixes CssStyleConfllicts.
//ref is ... something for counting..?
import TheKeys from '@/components/TheKeys.vue'
import TheEvents from '@/components/TheEvents.vue'
</script>

<style scoped></style>
