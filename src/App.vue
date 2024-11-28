<script setup>
import Order from "./components/Order.vue";
</script>

<template>
  <div class="flex container bd">
    <div class="A bd">
      <Order />
    </div>
    <div class="B bd">B</div>
  </div>
</template>

<style>
.container {
  padding: 2% 12%;
  gap: 1rem;
  .A {
    flex: 0.7;
  }
  .B {
    flex: 0.3;
  }
}
</style>
