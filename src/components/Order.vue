<script setup>
const props = defineProps({
  cartItemNumber: Number,
  epmty: Boolean,
});
</script>

<template>
  <div class="order">
    <div>
      <h3>Your Cart ( {{ cartItemNumber }} )</h3>
    </div>
    <div></div>
  </div>
</template>

<style lang="css" scoped>
h3 {
  color: var(--red);
}
.order {
  min-height: 200px;
  width: 300px;
  padding: 1%;
  background-color: #fff;
  border-radius: 0.625rem;
}
</style>
