<script setup>
import { ref } from "vue";
import Order from "./components/Order.vue";
import Dessert from "./components/Dessert.vue";

const totalItemsCount = ref(0);

function handleMinus() {}
function handlePlus() {}
</script>

<template>
  <div class="flex container">
    <div class="A bd">
      <Dessert  />
    </div>
    <div class="B bd">
      <Order :cart-item-number="totalItemsCount" />
    </div>
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
