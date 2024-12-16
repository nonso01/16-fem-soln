<script setup>
import { ref } from "vue";
import Order from "./components/Order.vue";
import Dessert from "./components/Dessert.vue";

const log = console.log;
const quantities = ref({});
const isQuantityVisible = ref({});
const notEmpty = ref(!false);
const orderData = ref([]);

function handleMinus(name, price) {
  if (!isQuantityVisible.value[name]) return;
  // Don't decrement if not visible
  if (quantities.value[name] > 0) {
    quantities.value[name]--;
  }

  quantities.value[name] === 0
    ? (isQuantityVisible.value[name] = false)
    : void 0;

  log(quantities.value);
  log(price);
}
function handlePlus(name, price) {
  if (!isQuantityVisible.value[name]) return;
  // Don't increment if not visible
  quantities.value[name] = (quantities.value[name] || 0) + 1;

  log(quantities.value);
  log(price);
}

function handleIsQuantityVisible(name) {
  isQuantityVisible.value[name] = !isQuantityVisible.value[name];

  // Optionally, reset to 0 if hiding, or initialize if showing
  if (!isQuantityVisible[name]) {
    quantities.value[name] = 0;
  } else if (!(name in quantities.value)) {
    quantities.value[name] = 0;
  }
}

function processOreder() {}
</script>

<template>
  <div class="flex container">
    <div class="A bd">
      <Dessert
        :quantities="quantities"
        :handle-minus="handleMinus"
        :handle-plus="handlePlus"
        :handle-is-quantity-visible="handleIsQuantityVisible"
        :is-quantity-visible="isQuantityVisible"
      />
    </div>
    <div class="B bd">
      <Order :not-empty="notEmpty" />
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
