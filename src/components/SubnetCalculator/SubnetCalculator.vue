<template>
  <div class="subnet-calculator">
    <h2>Калькулятор подсетей</h2>
    
    <form @submit.prevent="calculate" class="calculator-form">
      <UiField label="IP адрес:">
        <UiInput
          v-model="ipAddress"
          placeholder="192.168.1.150"
          :class="{ 'error': !isValidIp && ipAddress }"
          @keyup.enter="calculate"
        />
        <span v-if="!isValidIp && ipAddress" class="error-message">
          Неверный формат IP адреса
        </span>
      </UiField>

      <UiField label="Маска подсети:">
        <UiSelect
          v-model="selectedMask"
          :options="maskOptions"
          @keyup.enter="calculate"
        />
      </UiField>

      <UiButton
        type="submit"
        :disabled="!isFormValid"
        layout="primary"
      >
        Рассчитать
      </UiButton>
    </form>

    <div v-if="results" class="results">
      <h3>Результаты:</h3>
      <div class="result-item">
        <strong>IP адрес:</strong> {{ results.ip }}
      </div>
      <div class="result-item">
        <strong>Маска:</strong> {{ results.mask }}
      </div>
      <div class="result-item">
        <strong>Адрес сети:</strong> {{ results.networkAddress }}
      </div>
      <div class="result-item">
        <strong>Количество адресов:</strong> {{ results.addressesCount }}
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref, computed } from 'vue'
import UiButton from './UiButton.vue'
import UiInput from './UiInput.vue'
import UiField from './UiField.vue'
import UiSelect from './UiSelect.vue'
import { MASK_OPTIONS } from '../../utils/maskOptions'
import { isIpValid } from '../../utils/ipValidation'
import { getNetworkAddress, getAddressesCount } from '../../utils/networkCalculations'

const maskOptions = MASK_OPTIONS.map(option => option.label);

interface CalculationResult {
  ip: string
  mask: string
  networkAddress: string
  addressesCount: number
}

const ipAddress = ref('192.168.1.150')
const selectedMask = ref('255.255.255.0')
const results = ref<CalculationResult | null>(null)

const isValidIp = computed(() => isIpValid(ipAddress.value))
const isFormValid = computed(() => isValidIp.value && selectedMask.value)

function calculate() {
  if (!isFormValid.value) return

  results.value = {
    ip: ipAddress.value,
    mask: selectedMask.value,
    networkAddress: getNetworkAddress(ipAddress.value, selectedMask.value),
    addressesCount: getAddressesCount(selectedMask.value)
  }
}
</script>

<style scoped>
.subnet-calculator {
  max-width: 500px;
  margin: 0 auto;
  padding: 20px;
  font-family: Arial, sans-serif;
}

.calculator-form {
  display: flex;
  flex-direction: column;
  gap: 16px;
  margin-bottom: 24px;
}

.error-message {
  color: var(--color-error);
  font-size: 12px;
}

.results {
  padding: 16px;
  background-color: var(--color-background-soft);
  border-radius: 8px;
  border: 1px solid var(--color-border);
}

.results h3 {
  margin-top: 0;
  margin-bottom: 16px;
  color: var(--color-heading);
}

.result-item {
  margin-bottom: 8px;
  padding: 4px 0;
}
</style>
