<template>
  <div class="ui-field">
    <label v-if="label" class="ui-field-label">{{ label }}</label>
    <div class="ui-field-content">
      <slot></slot>
    </div>
  </div>
</template>

<script setup lang="ts">
defineProps<{
  label?: string
}>()
</script>

<style scoped>
.ui-field {
  display: flex;
  flex-direction: column;
  gap: 8px;
}

.ui-field-label {
  font-weight: bold;
  color: var(--color-black);
}
</style>
