<script setup>
import { ref } from "vue";

const props = defineProps({
  totalQuantity: Number,
  notEmpty: Boolean,
  total: Number,
  data: Object,
  handleCancelOrderItem: Function,
  handleConfirmOrder: Function,
});
</script>

<template>
  <div class="order flex col btw trans">
    <div class="title">
      <h3>Your Cart ({{ totalQuantity || 0 }})</h3>
    </div>
    <div class="items">
      <div v-if="!notEmpty" class="flex center col">
        <img src="/images/illustration-empty-cart.svg" alt="empty cart" />

        <p>Your added items will appear here</p>
      </div>

      <div v-if="notEmpty" class="store">
        <div
          class="s-item flex btw center"
          v-for="item in Object.entries(data)"
        >
          <div class="selected flex btw">
            <h6>{{ item[0] }}</h6>
            <p>
              <span class="q">{{ item[1].quantity }}x</span>
              <span class="p">${{ item[1].price.toFixed(2) }}</span>
              <span class="t">
                ${{ (item[1].quantity * item[1].price).toFixed(2) }}</span
              >
            </p>
          </div>
          <div
            class="cancel flex center trans bd"
            @click="handleCancelOrderItem(item[0])"
          >
            <img src="/images/icon-remove-item.svg" alt="cancel svg" />
          </div>
        </div>

        <div class="order-total flex col even">
          <div class="flex btw center">
            <p>Order Total</p>
            <h3>${{ total || 10 }}</h3>
          </div>
          <div class="carbon flex center even">
            <img src="/images/icon-carbon-neutral.svg" alt="carbon" />
            <span>This is a <b>carbon-neutral</b> delivery</span>
          </div>
          <div class="btn flex center" @click="handleConfirmOrder">
            Confirm Order
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style lang="css" scoped>
h3 {
  color: var(--red);
}
.order {
  min-height: 200px;
  /* width: 300px; */

  padding: 3.5% 3.5%;
  background-color: #fff;
  border-radius: 0.625rem;

  .items {
    p {
      color: var(--rose-300);
      font-weight: bold;
      font-size: 0.8rem;
    }
  }
}

.store {
  /* height: 40px; */

  .order-total {
    /* border: 2px solid; */
    height: 200px;

    h3 {
      color: var(--rose-900);
    }
    p {
      color: var(--rose-500);
    }
  }

  .carbon {
    background-color: var(--rose-100);
    height: 50px;
    font-size: 0.8rem;
    border-radius: 0.6rem;
    padding-inline: 7%;
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

.s-item {
  border-bottom: 2px solid var(--rose-100);
  height: 70px;
  margin-block: 1%;

  span {
    margin: 3%;
  }

  .selected {
    flex-direction: column;
    width: 60%;
    height: 60%;

    .q {
      color: var(--red);
    }
    .p {
      font-weight: 600;
    }
  }

  .cancel {
    width: 20px;
    height: 20px;
    border-radius: 50%;
    border-color: var(--rose-300);
    cursor: pointer;

    &:hover {
      filter: grayscale(70%);
    }
  }
}
</style>
