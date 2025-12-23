<template>
  <select class="ui-select" :value="modelValue" @change="updateValue" :disabled="isDisabled">
    <option v-for="option in options" :key="option" :value="option">{{ option }}</option>
  </select>
</template>

<script setup lang="ts">
defineProps<{
  modelValue: string
  isDisabled?: boolean
  options: string[]
}>()

const emit = defineEmits<{
  "update:modelValue": [value: string]
}>()

function updateValue(event: Event) {
  const target = event.target as HTMLSelectElement
  emit("update:modelValue", target.value)
}
</script>

<style scoped>
.ui-select {
  padding: 8px 12px;
  border: 1px solid var(--color-gray);
  border-radius: 4px;
  font-size: 14px;
}
</style>
