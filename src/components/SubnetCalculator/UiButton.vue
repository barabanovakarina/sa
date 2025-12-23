<template>
  <button class="ui-button" :disabled="isDisabled" :type="type">
    <slot></slot>
  </button>
</template>

<script setup lang="ts">
defineProps<{
  isDisabled?: boolean
  type?: string
  layout?: string
}>()
</script>

<style scoped>
.ui-button {
  padding: 12px 24px;
  background: var(--color-primary);
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

.ui-button:disabled {
  background: var(--color-gray);
  cursor: not-allowed;
}
</style>
