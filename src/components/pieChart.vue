<template>
  <div id="chart" style="width: 100%">
    <apexchart
      type="pie"
      height="350"
      :options="option"
      :series="data"
    ></apexchart>
  </div>
</template>
<script lang="ts">
import { defineComponent, ref } from "vue";
import VueApexCharts from "vue3-apexcharts";

export default defineComponent({
  components: {
    apexchart: VueApexCharts,
  },
  setup() {
    let data = ref([10, 34, 67, 90, 78]);

    let option = ref({
      chart: {
        width: 350,
        type: "pie",
      },
      labels: ["Team A", "Team B", "Team C", "Team D", "Team E"],
      responsive: [
        {
          breakpoint: 480,
          options: {
            chart: {
              width: 200,
            },
            legend: {
              position: "bottom",
            },
          },
        },
      ],
      title: {
        text: "Pie Chart",
        align: "left",
      },
    });
    return { data, option };
  },
});
</script>
