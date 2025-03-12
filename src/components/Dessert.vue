<script setup>
import { onMounted, ref } from "vue";

const props = defineProps({
  handlePlus: Function,
  handleMinus: Function,
  handleRemoveCart: Function,
  handleIsQuantityVisible: Function,
  quantities: Object,
  isQuantityVisible: Object,
});
const log = console.log;

const data = ref(null);

onMounted(() => {
  fetch("./data.json")
    .then((res) => res.json())
    .then((val) => {
      data.value = val;
    })
    .catch((error) => console.warn(error));
});
</script>

<template>
  <div class="dessert flex col btw">
    <h2 class="rose-900">Desserts</h2>
    <div class="cover">
      <div
        class="items flex col btw"
        v-for="{ category, image, name, price } in data"
        :key="category"
      >
        <div
          class="content"
          :class="{ colored: isQuantityVisible[name] }"
          :style="{ '--bg': `url(${image.desktop})` }"
        >
          <div class="add flex center bd">
            <div
              class="flex even prev"
              :class="{ hide: isQuantityVisible[name] }"
              @click="handleIsQuantityVisible(name)"
            >
              <img src="/images/icon-add-to-cart.svg" alt="at-to-cart" />
              <span class="rose-900 trans">Add to cart</span>
            </div>

            <div
              class="next flex even"
              :class="{ hide: !isQuantityVisible[name] }"
            >
              <img
                src="/images/icon-decrement-quantity.svg"
                alt="minus"
                class="trans"
                @click="handleMinus(name, price, image.thumbnail)"
              />
              <span>{{ quantities[name] || 0 }}</span>
              <img
                src="/images/icon-increment-quantity.svg"
                alt="plus"
                class="trans"
                @click="handlePlus(name, price, image.thumbnail)"
              />
            </div>
          </div>
        </div>
        <div class="details flex even">
          <p class="cat">{{ category }}</p>
          <p class="name">{{ name }}</p>
          <p class="price">${{ price.toFixed(2) }}</p>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
img {
  cursor: pointer;
}
.dessert {
  height: 100%;

  .details {
    /* border-color: red; */
    height: 21%;
    flex-direction: column;
    font-weight: 600;
    /* width: 90%; */

    p {
      font-size: 0.7rem;
    }

    .cat {
      color: var(--rose-500);
    }
    .name {
      color: var(--rose-900);
      font-size: 0.8rem;
    }
    .price {
      color: var(--red);
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
    .content {
      border: 2px solid transparent;
      transition-duration: 100ms;
      position: relative;
      width: 90%;
      height: 68%;
      background-image: var(--bg);
      background-size: cover;
      background-repeat: no-repeat;
      background-clip: content-box; /* enhances the bg curvature */
      border-radius: 0.65rem;

      &.colored {
        border-color: var(--red);
      }
    }
  }

  .add {
    border-width: 1px;
    position: absolute;
    bottom: -10%;
    left: 50%;
    transform: translate(-50%, 0%);
    width: 70%;
    height: 20%;
    border-radius: 1.5rem;
    background-color: white;

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

@media screen and (max-width: 600px) {
  #app {
    h2 {
      margin: 3% 6%;
      font-size: 1.8rem;
    }
    .cover {
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      gap: 0.8rem;

      .items {
        width: 90%;
        height: 21.9rem;

        .content {
          /* width: 100%; */
          align-self: center;
          background-position: 100%;
        }

        .add {
          width: 60%;

          span {
            font-size: 0.9rem;
          }
        }

        .details {
          height: 23%;
          padding-left: 5%;
          .cat {
            font-size: 0.9rem;
          }
          .name {
            font-size: 0.95rem;
          }
          .price {
            font-size: 1rem;
          }
        }
      }
    }
  }
}
</style>
