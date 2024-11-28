<script setup>
import { onMounted, ref } from "vue";

// const props = defineProps({})
const log = console.log;

const data = ref(null);

onMounted(() => {
  fetch("./data.json")
    .then((res) => res.json())
    .then((val) => {
      log(val);
      data.value = val;
    })
    .catch((error) => console.warn(error));
});
</script>

<template>
  <div class="dessert flex col btw">
    <h2>Desserts</h2>
    <div class="cover">
      <div class="items" v-for="{ category, image, name, price } in data">
        <!-- <img :src="image.desktop" /> -->
        <div class="content" :style="{ '--bg': `url(${image.tablet})` }">
          <div class="add">add to cart</div>
        </div>
        <div class="details">
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

  p {
    font-size: 0.6rem;
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
      width: 85%;
      height: 75%;
      background-image: var(--bg);
      background-size: cover;
    }
  }
}
</style>
