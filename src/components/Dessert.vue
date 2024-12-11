<script setup>
import { onMounted, ref } from "vue";

const props = defineProps({
  handlePlus: Function,
  handleMinus: Function,
  handleAddcart: Function,
  handleRemoveCart: Function,
  quantities: Object,
});
const log = console.log;

const data = ref(null);
const cartItems = ref(null);

onMounted(() => {
  fetch("./data.json")
    .then((res) => res.json())
    .then((val) => {
      data.value = val;
    })
    .catch((error) => console.warn(error));
});

// function handleAddcart() {
//   const prev = document.querySelector(".add .prev");
//   // const next = document.querySelector(".add .next");
//   // prev.classList.toggle("hide");
//   // next.classList.toggle("hide");
//   log(prev);
// }
</script>

<template>
  <div class="dessert flex col btw">
    <h2 class="rose-900">Desserts</h2>
    <div class="cover">
      <div
        class="items flex col center btw"
        v-for="{ category, image, name, price } in data"
        :key="category"
      >
        <div class="content" :style="{ '--bg': `url(${image.tablet})` }">
          <div class="add flex center bd">
            <div class="flex even prev" @click="handleAddcart(category)">
              <img src="/images/icon-add-to-cart.svg" alt="at-to-cart" />
              <span class="rose-900 trans">Add to cart</span>
            </div>

            <div class="next flex even hide">
              <img
                src="/images/icon-decrement-quantity.svg"
                alt="minus"
                class="trans"
                @click="handleMinus"
              />
              <span>{{ 0 }}</span>
              <img
                src="/images/icon-increment-quantity.svg"
                alt="plus"
                class="trans"
                @click="handlePlus"
              />
            </div>
          </div>
        </div>
        <div class="details bd">
          <p>{{ category }}</p>
          <p>{{ name }}</p>
          <p>{{ price }}</p>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.dessert {
  height: 100%;

  .details {
    width: 90%;

    p {
      font-size: 0.7rem;
    }
  }

  .cover {
    flex: 0.99;
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    grid-template-rows: repeat(3, 1fr);
    /* using fixed size against browser console */
    gap: 0.5rem;
  }

  .items {
    /* border-radius: 0.625rem; */

    .content {
      position: relative;
      width: 78%;
      height: 68%;
      background-image: var(--bg);
      background-size: cover;
      border-radius: 0.25rem;
    }
  }

  .add {
    position: absolute;
    bottom: -10%;
    left: 50%;
    transform: translate(-50%, 0%);
    width: 70%;
    height: 20%;
    border-radius: 1.5rem;
    background-color: white;
    /* border-width: 1.99px; */

    span {
      margin-inline: 0.625rem;
      font-size: 0.8rem;
      font-weight: 600;

      &:not(.next span):hover {
        color: var(--red);
      }
    }

    &:has(.next:not(.hide.next)) {
      background-color: var(--red);
    }

    .next {
      width: 100%;
      color: var(--rose-50);

      img:hover {
        /* border: 2px solid; */
        scale: 1.8;
      }
    }
  }
}
</style>
