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
        data: [
          {
            x: "category A",
            y: 10,
          },
          {
            x: "category B",
            y: 18,
          },
          {
            x: "category C",
            y: 13,
          },
        ],
      },
    ]);

    let option = ref({
      chart: {
        type: "bar",
        height: 350,
      },
      title: {
        text: "bar Chart",
        align: "left",
      },
    });
    return { data, option };
  },
});
</script>
