<script setup>
import { ref } from "vue";
import Order from "./components/Order.vue";
import Dessert from "./components/Dessert.vue";

const log = console.log;
const quantities = ref({});
const isQuantityVisible = ref({});
const notEmpty = ref(false);
const orderData = ref({});
const orderTotalCost = ref(0);

function handleMinus(name, price) {
  if (!isQuantityVisible.value[name]) return;
  // Don't decrement if not visible
  if (quantities.value[name] > 0) {
    quantities.value[name]--;
  }

  quantities.value[name] === 0
    ? (isQuantityVisible.value[name] = false)
    : void 0;

  let test = processOreder(name, price);

  handleIsNotEmpty();
  processOrederTotal();
}

function handlePlus(name, price) {
  if (!isQuantityVisible.value[name]) return;
  // Don't increment if not visible
  quantities.value[name] = (quantities.value[name] || 0) + 1;

  let test = processOreder(name, price);

  handleIsNotEmpty();
  processOrederTotal();
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

function handleIsNotEmpty() {
  Object.entries(orderData.value).length === 0
    ? (notEmpty.value = false)
    : (notEmpty.value = true);
}

function handleCancelOrderItem(name) {
  if (orderData.value[name].quantity !== 0) {
    delete orderData.value[name];
    quantities.value[name] = 0;
    isQuantityVisible.value[name] = false;
  }
}

function processOreder(name, price) {
  orderData.value[name] = {
    quantity: quantities.value[name],
    price,
  };

  orderData.value[name].quantity === 0 ? delete orderData.value[name] : void 0;

  return orderData.value;
}

function processOrederTotal() {
  let numbers = [];
  Object.entries(orderData.value).forEach((item) => {
    let mul = item[1].price * item[1].quantity;
    numbers.push(mul);
  });
  orderTotalCost.value = numbers.reduce((acc, val) => acc + val, 0);
  console.table([numbers, orderTotalCost.value]);
}
</script>

<template>
  <div class="flex container">
    <div class="A">
      <Dessert
        :quantities="quantities"
        :handle-minus="handleMinus"
        :handle-plus="handlePlus"
        :handle-is-quantity-visible="handleIsQuantityVisible"
        :is-quantity-visible="isQuantityVisible"
      />
    </div>
    <div class="B">
      <Order
        :not-empty="notEmpty"
        :data="orderData"
        :total="orderTotalCost"
        :handleCancelOrderItem="handleCancelOrderItem"
      />
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
    flex: 0.28;
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
