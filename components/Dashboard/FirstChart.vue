<template>
  <UiCard>
    <UiTitle title="Security cases" level="h4" />
    <DoughnutChart :chartData="testData" />
  </UiCard>
</template>
<script setup lang="ts">
import { DoughnutChart } from 'vue-chart-3';
import { Chart, registerables } from "chart.js";

Chart.register(...registerables);

const testData = {
  labels: ['Open', 'Closed', 'In progress', 'Atention', 'Alert'],
  datasets: [
    {
      data: [30, 40, 60, 70, 5],
      backgroundColor: ['#77CEFF', '#0079AF', '#123E6B', '#97B0C4', '#A5C8ED'],
    },
  ],
};
</script>