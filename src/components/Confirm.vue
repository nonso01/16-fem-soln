<script setup>
const props = defineProps({
  finalData: Object,
  handleStartNewOrder: Function,
});
</script>

<template>
  <div class="confirm flex col btw">
    <div class="check flex col even bd">
      <div class="bd">
        <img src="/images/icon-order-confirmed.svg" alt="order confirmed" />
      </div>
      <div class="bd">
        <h1>Order Confirmed</h1>
        <p>We hope you enjoy your food!</p>
      </div>
    </div>

    <div class="receipt bd"></div>

    <div class="btn flex center bd">Start New Order</div>
  </div>
</template>

<style scoped>
.confirm {
  position: fixed;
  z-index: 10;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  width: 28.2rem;
  height: 34.4rem;
  padding: 0.5%;
  border-radius: 0.7rem;
  background-color: hsla(20, 50%, 98%, 0.85);
  backdrop-filter: blur(5px);

  .check {
    height: 30%;
  }

  .receipt {
    height: 55%;
  }

  .btn {
    height: 50px;
    background-color: var(--red);
    border-radius: 2rem;
    font-size: 0.8rem;
    font-weight: 600;
    color: var(--rose-100);
    cursor: pointer;
  }
}
</style>
