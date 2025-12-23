<template>
  <div class="home-page">
    <h1>Калькулятор подсетей</h1>
    <SubnetCalculator />
  </div>
</template>

<script setup lang="ts">
import SubnetCalculator from '../components/SubnetCalculator/SubnetCalculator.vue'
</script>

<style scoped>
.home-page {
  padding: 20px;
  max-width: 800px;
  margin: 0 auto;
}

h1 {
  text-align: center;
  color: var(--color-heading);
  margin-bottom: 32px;
}
</style>