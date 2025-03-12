<script setup>
import { ref } from "vue";
import Order from "./components/Order.vue";
import Dessert from "./components/Dessert.vue";
import Confirm from "./components/Confirm.vue";

const log = console.log;

const quantities = ref({});
const isQuantityVisible = ref({});
const notEmpty = ref(false);
const orderData = ref({});
const orderTotalCost = ref(0);
const orderTotalQuantity = ref(0);
const showOverlay = ref(false);
const showOC = ref(false);

function handleMinus(name, price, imageSrc) {
  if (!isQuantityVisible.value[name]) return;
  // Don't decrement if not visible
  if (quantities.value[name] > 0) {
    quantities.value[name]--;
  }

  quantities.value[name] === 0
    ? (isQuantityVisible.value[name] = false)
    : void 0;

  processOreder(name, price, imageSrc);

  handleIsNotEmpty();
  processOrederTotal();
}

function handlePlus(name, price, imageSrc) {
  if (!isQuantityVisible.value[name]) return;
  // Don't increment if not visible
  quantities.value[name] = (quantities.value[name] || 0) + 1;

  processOreder(name, price, imageSrc);

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

    handleIsNotEmpty();

    processOrederTotal();
  }
}

function handleConfirmOrder() {
  showOverlay.value = true;
}
function handleStartNewOrder() {
  showOverlay.value = false;

  setTimeout(() => {
    // reset to default
    showOC.value = true;
    notEmpty.value = false;
    orderData.value = {};
    quantities.value = {};
    isQuantityVisible.value = {};
    orderTotalCost.value = 0;
    orderTotalQuantity.value = 0;
  }, 600);

  setTimeout(() => {
    showOC.value = false;
  }, 1500);
}

function processOreder(name, price, imageSrc) {
  orderData.value[name] = {
    quantity: quantities.value[name],
    price,
    imageSrc,
  };

  orderData.value[name].quantity === 0 ? delete orderData.value[name] : void 0;

  return orderData.value;
}

function processOrederTotal() {
  let num = [];
  Object.entries(orderData.value).forEach((item) => {
    let mul = item[1].price * item[1].quantity;
    num.push(mul);
  });
  orderTotalCost.value = num.reduce((acc, val) => acc + val, 0);
  processOrederQuantity();
}

function processOrederQuantity() {
  let num = [];
  Object.entries(orderData.value).forEach((item) => {
    num.push(item[1].quantity);
  });
  orderTotalQuantity.value = num.reduce((acc, val) => acc + val, 0);
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
        :totalQuantity="orderTotalQuantity"
        :handleCancelOrderItem="handleCancelOrderItem"
        :handleConfirmOrder="handleConfirmOrder"
      />
    </div>
  </div>

  <Transition name="in">
    <Confirm
      v-if="showOverlay"
      :data="orderData"
      :total-cost="orderTotalCost"
      :handleStartNewOrder="handleStartNewOrder"
    />
  </Transition>

  <Transition>
    <div
      class="overlay"
      v-if="showOverlay"
      @click="
        () => {
          showOverlay = !showOverlay;
        }
      "
    ></div>
  </Transition>

  <Transition>
    <div class="o-c even center flex" v-if="showOC">
      <img src="/images/icon-order-confirmed.svg" alt="confirmed" />
      <p>Order Confirmed</p>
    </div>
  </Transition>
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

.overlay {
  height: 100lvh;
  width: 100lvw;
  position: fixed;
  top: 0;
  z-index: 5;
  background: #27272797;
  backdrop-filter: blur(0.3rem);
}

.o-c {
  position: fixed;
  top: 2%;
  left: 50%;
  transform: translate3d(-50%, -2%, 0);
  width: 14.4rem;
  height: 4.4rem;
  border-radius: 0.625rem;
  background-color: rgb(255, 255, 255);
  color: var(--rose-900);
  font-weight: bold;
  box-shadow: 0 0.25rem 1rem rgb(0 0 0 / 0.2);
}

.v-enter-active,
.v-leave-active {
  transition: opacity 0.25s ease;
}
.v-enter-from,
.v-leave-to {
  opacity: 0;
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

@media screen and (max-width: 600px) {
  #app {
    .container {
      flex-direction: column;

      .B {
        width: 85%;
        align-self: center;
      }
    }
  }
}
</style>
