<script setup>
const props = defineProps({
  data: Object,
  totalCost: Number,
  handleStartNewOrder: Function,
});
</script>

<template>
  <div class="confirm flex col btw">
    <div class="check flex col even">
      <div class="">
        <img src="/images/icon-order-confirmed.svg" alt="order confirmed" />
      </div>
      <div class="">
        <h1>Order Confirmed</h1>
        <p>We hope you enjoy your food!</p>
      </div>
    </div>

    <div class="receipt flex col btw">
      <div class="items">
        <div class="item flex btw" v-for="item in Object.entries(data)">
          <div class="p flex center">
            <div class="i">
              <img :src="item[1].imageSrc" alt="" />
            </div>
            <div class="q flex col btw">
              <p class="main">{{ item[0] }}</p>
              <p>
                <span class="quantity">{{ item[1].quantity }}x</span>
                <span
                  >${{ (item[1].quantity * item[1].price).toFixed(2) }}</span
                >
              </p>
            </div>
          </div>

          <h5>${{ (item[1].quantity * item[1].price).toFixed(2) }}</h5>
        </div>
      </div>
      <div class="flex btw center">
        <p>Order Total</p>
        <h2>${{ totalCost.toFixed(2) || 0 }}</h2>
      </div>
    </div>

    <div class="btn flex center" @click="handleStartNewOrder">
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
  backdrop-filter: blur(.3rem);

  h1,
  h2,
  h5 {
    color: var(--rose-900);
  }
  h5 {
    align-self: center;
    margin-inline: 1%;
  }
  p {
    color: var(--rose-500);
    font-size: 0.85rem;
  }

  .check {
    height: 28%;
  }

  .receipt {
    height: 55%;
    padding: 2%;
    background-color: hsla(13, 29%, 94%, 0.794);
    border-radius: 0.6rem;

    .p {
      width: 80%;
    }

    .q {
      margin-left: 3%;
      width: 80%;
      .main {
        color: var(--rose-900);
      }
      .quantity {
        color: var(--red);
        margin-right: 5%;
      }
    }

    .i {
      height: 2.81rem;
      width: 2.81rem;
      background: #000;
      img {
        width: 100%;
        height: 100%;
      }
    }

    .items {
      min-height: 80%;
      overflow: auto;
      &::-webkit-scrollbar-track {
        /* box-shadow: inset 0 0 6px rgb(0 0 0 / 0.3);
        border-radius: 0.625rem;
        background-color: #f5f5f5; */
        display: none;
      }
      &::-webkit-scrollbar {
        /* width: 0.2rem;
        background-color: #f5f5f5; */
        display: none;
      }
      &::-webkit-scrollbar-thumb {
        /* border-radius: 0.2rem;
        box-shadow: inset 0 0 6px rgb(0 0 0 / 0.3);
        background-color: var(--rose-300); */
        display: none;
      }
    }

    .item {
      height: 3.38rem;
      margin-block: 2.5%;
      border-bottom: 1px solid var(--rose-300);
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
