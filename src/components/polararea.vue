<template>
  <div>
    <LineChart :chartData="lineChartData" />
  </div>
</template>
<script lang="ts">
import { defineComponent, reactive } from "vue";
import { Chart, registerables } from "chart.js";
import { LineChart } from "vue-chart-3";

Chart.register(...registerables);

export default defineComponent({
  components: {
    LineChart,
  },
  setup() {
    const lineChartData = reactive({
      labels: [
        "monday",
        "tuesday",
        "wednesday",
        "thursday",
        "friday",
        "saturday",
        "sunday",
      ],
      datasets: [
        {
          label: "Stocks",
          data: [12, 34, 45, 67, 23, 98, 34],
          backgroundColor: "#77CEFF",
          fill: true,
        },
        {
          label: "stock 2",
          data: [22, 43, 15, 57, 73, 28, 34],
          backgroundColor: "#0079AF",
          fill: true,
        },
      ],
    });
    return {
      lineChartData,
    };
  },
});
</script>
