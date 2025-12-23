<template>
  <div id="app">
    <HomePage />
  </div>
</template>

<script setup lang="ts">
import HomePage from './pages/HomePage.vue'
</script>

<style>
:root {
  --color-primary: #006cbb;
  --color-primary-dark: #005a9c;
  --color-error: #d40019;
  --color-success: #01bd78;
  --color-white: #fff;
  --color-gray: #ccc;
  --color-black: #000;
  --color-text: #333;
  --color-heading: #222;
  --color-border: #ddd;
  --color-background-soft: #f9f9f9;
}

* {
  box-sizing: border-box;
}

body {
  margin: 0;
  padding: 0;
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
  background-color: var(--color-white);
  color: var(--color-text);
}
</style>