<script setup>
const props = defineProps({
  cartItemNumber: Number,
  epmty: Boolean,
});
</script>

<template>
  <div class="order flex col btw">
    <div class="title">
      <h3>Your Cart ({{ cartItemNumber }})</h3>
    </div>
    <div class="items">
        <div v-if="!epmty" class="flex center col">
            <img src="/images/illustration-empty-cart.svg" alt="empty cart">

            <p>Your added items will appear here</p>
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
  width: 300px;
  padding: 2.5% 1.5%;
  background-color: #fff;
  border-radius: 0.625rem;

  .items {
    p {
        color: var(--rose-300);
        font-weight: bold;
        font-size: .8rem;
    }
  }
}
</style>
