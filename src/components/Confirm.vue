<script setup>
const props = defineProps({
  finalData: Object,
  totalCost: Number,
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

    <div class="receipt flex col btw">
      <div class="items bd">
        <div class="item flex btw">
          <div class="p flex center bd">
            <div class="i">
              <img src="" alt="" />
            </div>
            <div class="q flex col btw bd">
              <p>yellow</p>
              <p><span>quantity</span><span>$price</span></p>
            </div>
          </div>

          <h4>$0</h4>
        </div>
      </div>
      <div class="bd flex btw center">
        <p>Order Total</p>
        <h2>${{ totalCost || 0 }}</h2>
      </div>
    </div>

    <div class="btn flex center bd" @click="handleStartNewOrder">
      Start New Order
    </div>
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
  padding: 0.8%;
  border-radius: 0.8rem;
  background-color: hsla(20, 50%, 98%, 0.85);
  backdrop-filter: blur(5px);

  h1,
  h2,
  h4 {
    color: var(--rose-900);
  }
  h4 {
    align-self: center;
  }
  p {
    color: var(--rose-500);
    font-size: 0.85rem;
  }

  .check {
    height: 30%;
  }

  .receipt {
    height: 55%;
    padding: 2%;

    .p {
      width: 80%;
    }
    .q {
      margin-left: 3%;
      width: 80%;
    }

    .i  {
      height: 45px;
      width: 45px;
      background: #000;
    }

    .items {
      min-height: 80%;
    }

    .item {
      height: 3.38rem;
      margin-block: 1%;
    }
  }

  .btn {
    height: 3.13rem;
    background-color: var(--red);
    border-radius: 2rem;
    font-size: 0.9rem;
    font-weight: 600;
    color: var(--rose-100);
    cursor: pointer;
  }
}
</style>
