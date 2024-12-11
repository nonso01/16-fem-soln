<script setup>
import { ref } from "vue";
import Order from "./components/Order.vue";
import Dessert from "./components/Dessert.vue";

const totalItemsCount = ref(0);
const quantities = ref({});
const isQuantityVisible = ref({});

function handleMinus(category) {
  if (!isQuantityVisible.value[category]) return;
  // Don't decrement if not visible
  if (quantities.value[category] > 0) {
    quantities.value[category]--;
  }
}
function handlePlus(category) {
  if (!isQuantityVisible.value[category]) return;
  // Don't increment if not visible
  quantities.value[category] = (quantities.value[category] || 0) + 1;
}

function handleIsQuantityVisible(category) {
  isQuantityVisible.value[category] = !isQuantityVisible.value[category];

  // Optionally, reset to 0 if hiding, or initialize if showing
  if (!isQuantityVisible[category]) {
    quantities.value[category] = 0;
  } else if (!(category in quantities.value)) {
    quantities.value[category] = 0;
  }
}

function handleAddcart(category) {
  if (!quantities.value[category]) {
    quantities.value[category] = 1;
  } else {
    quantities.value[category]++;
  }
  console.log(quantities.value);
}
</script>

<template>
  <div class="flex container">
    <div class="A bd">
      <Dessert :quantities="quantities" :handle-addcart="handleAddcart" />
    </div>
    <div class="B bd">
      <Order :cart-item-number="totalItemsCount" />
    </div>
  </div>
</template>

<style>
.container {
  /* padding: 1% 20%; */
  gap: 1rem;

  .A {
    flex: 0.7;
  }
  .B {
    flex: 0.3;
  }
}

@media screen and (min-width: 1200px) {
  /* better than 1920px */
  #app {
    display: flex;
    justify-content: center;
    align-items: center;

    .container {
      width: 1155px;
      min-height: 990px;
      margin-block: 2%;
    }
  }
}
</style>
