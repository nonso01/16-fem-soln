<script setup>
import { ref } from "vue";
import Order from "./components/Order.vue";
import Dessert from "./components/Dessert.vue";

const totalItemsCount = ref(0)
</script>

<template>
  <div class="flex container bd">
    <div class="A bd">
      <!-- <Order :cart-item-number="totalItemsCount" /> -->
       <Dessert />
    </div>
    <div class="B bd">B</div>
  </div>
</template>

<style>
.container {
  padding: 1% 20%;
  gap: 1rem;
  .A {
    flex: 0.7;
  }
  .B {
    flex: 0.3;
  }
}
</style>
