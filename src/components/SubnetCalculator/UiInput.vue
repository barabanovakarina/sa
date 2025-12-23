<template>
  <input class="ui-input" :value="modelValue" @input="updateValue" :disabled="isDisabled" :placeholder="placeholder">
</template>

<script setup lang="ts">
defineProps<{
  modelValue: string
  isDisabled?: boolean
  placeholder?: string
}>()

const emit = defineEmits<{
  "update:modelValue": [value: string]
}>()

function updateValue(event: Event) {
  const target = event.target as HTMLInputElement
  emit("update:modelValue", target.value)
}
</script>

<style scoped>
.ui-input {
  padding: 8px 12px;
  border: 1px solid var(--color-gray);
  border-radius: 4px;
  font-size: 14px;
}
</style>
