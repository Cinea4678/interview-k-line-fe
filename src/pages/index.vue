<script setup lang="ts" generic="T extends any, O extends any">
import type { EChartsOption } from 'echarts'
import { CandlestickChart } from 'echarts/charts'
import {
  GridComponent,
  LegendComponent,
  TitleComponent,
  TooltipComponent,
} from 'echarts/components'
import { use } from 'echarts/core'
import { CanvasRenderer } from 'echarts/renderers'
import VChart from 'vue-echarts'

use([
  TitleComponent,
  TooltipComponent,
  LegendComponent,
  GridComponent,
  CandlestickChart,
  CanvasRenderer,
])

const { data: eventSourceData } = useEventSource('https://sel-arm.fmeow.com:5203/trade/sse')
watch(eventSourceData, (d) => {
  // 在这里处理收到的数据
  console.log(d)
})

const chartOption = computed<EChartsOption>(() => {
  return {
    title: {
      text: 'K线图',
    },
    tooltip: {},
    legend: { data: [] },
    xAxis: { data: [] },
    yAxis: { data: [] },
    series: [
      {
        type: 'candlestick',
        // 二维数组的每一数组项（上例中的每行）是渲染一个box，它含有四个量值，依次是：
        // [open, close, lowest, highest] （即：[开盘值, 收盘值, 最低值, 最高值]）
        data: [
          [20, 34, 10, 38],
          [40, 35, 30, 50],
          [31, 38, 33, 44],
          [38, 15, 5, 42],
        ],
      },
    ],
  }
})
</script>

<template>
  <VChart class="h-100vh" :option="chartOption" autoresize />
</template>
