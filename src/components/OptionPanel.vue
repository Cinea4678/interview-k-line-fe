<script setup lang="ts">
const symbols = [
  { name: 'BTC/USDT', code: 'btcusdt' },
  { name: 'ETH/USDT', code: 'ethusdt' },
  { name: 'BNB/USDT', code: 'bnbusdt' },
  { name: 'DOGE/USDT', code: 'dogeusdt' },
] as const

const selectedSymbol = ref<typeof symbols[number]['code']>('btcusdt')
const windowSize = ref(1)
</script>

<template>
  <div class="w-full flex items-center justify-center gap-8">
    <div class="flex items-center gap-3">
      <label>选择标的</label>
      <Select v-model="selectedSymbol" :options="symbols as unknown as any[]" option-label="name" option-value="code" placeholder="选择一个标的" />
    </div>

    <div class="flex items-center gap-3">
      <label>时间窗口(秒)</label>
      <InputNumber v-model="windowSize" placeholder="输入时间窗口" />
    </div>
  </div>
</template>
