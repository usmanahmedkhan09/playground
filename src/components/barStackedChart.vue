<template>
  <div id="chart" style="width: 100%">
    <apexchart
      type="bar"
      :options="option"
      height="350"
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
    let data = ref([
      {
        name: "PRODUCT A",
        data: [44, 55, 41, 67, 22, 43, 21, 49],
      },
      {
        name: "PRODUCT B",
        data: [13, 23, 20, 8, 13, 27, 33, 12],
      },
      {
        name: "PRODUCT C",
        data: [11, 17, 15, 15, 21, 14, 15, 13],
      },
    ]);

    let option = ref({
      chart: {
        type: "bar",
        height: 350,
        stacked: true,
        stackType: "100%",
      },
      title: {
        text: "bar Stacked Chart",
        align: "left",
      },
      xaxis: {
        categories: [
          "2011",
          "2011",
          "2011",
          "2011",
          "2012",
          "2012",
          "2012",
          "2012",
        ],
      },
    });
    return { data, option };
  },
});
</script>
