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
            <h3>${{ total || 0 }}</h3>
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
  min-height: 12.5rem;

  padding: 3.5% 3.5%;
  margin-bottom: 5%;
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
  .order-total {
    /* border: 2px solid; */
    height: 12.5rem;

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
    span,
    b {
      color: var(--rose-900);
    }
  }

  .btn {
    height: 3.13rem;
    background-color: var(--red);
    border-radius: 2rem;
    font-size: 0.8rem;
    font-weight: 600;
    color: var(--rose-100);
    cursor: pointer;

    &:hover {
      filter: grayscale(30%);
    }
  }
}

.s-item {
  border-bottom: 2px solid var(--rose-100);
  height: 4.4rem;
  margin-block: 1%;

  span {
    margin: 3%;
  }

  .selected {
    flex-direction: column;
    width: 60%;
    height: 60%;

    h6 {
      color: var(--rose-900);
    }

    .q {
      color: var(--red);
    }
    .p {
      font-weight: 600;
    }
  }

  .cancel {
    width: 1.25rem;
    height: 1.25rem;
    border-radius: 50%;
    border-color: var(--rose-300);
    cursor: pointer;

    &:hover {
      filter: grayscale(70%);
    }
  }
}

/* @media screen and (max-width: 600px) {
  #app {
    .order {
    
    }
  }
} */
</style>
