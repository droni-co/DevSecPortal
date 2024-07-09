<template>
  <UiCard>
    <LineChart :chartData="testData" :options="options" />
  </UiCard>
</template>
<script setup lang="ts">
import { LineChart } from 'vue-chart-3';
import { Chart, registerables } from "chart.js";

Chart.register(...registerables);

const testData = {
  labels: ['Open', 'Closed', 'In progress', 'Atention', 'Alert'],
  datasets: [
    {
      data: [30, 40, 60, 70, 35],
      backgroundColor: ['#77CEFF', '#0079AF', '#123E6B', '#97B0C4', '#A5C8ED'],
    },
  ],
};
const options = {
    responsive: true,
    plugins: {
      title: {
        display: true,
        text: 'Commits and updates per day'
      },
    },
    interaction: {
      intersect: false,
    },
    scales: {
      x: {
        display: true,
        title: {
          display: true
        }
      },
      y: {
        display: true,
        title: {
          display: true,
          text: 'Value'
        },
        suggestedMin: -10,
        suggestedMax: 200
      }
    }
  };
</script>