<script setup>
import { ref } from "vue";
const count = ref(0);
</script>
<template>
  <div>
    <h1>This is my test components</h1>
    <button @click="count++">+</button>
    <button @click="count--">-</button>
    <p>Handle Count: {{ count }}</p>
  </div>
</template>
<style scoped>
h1 {
  font-size: 20px;
  color: red;
}
</style>
