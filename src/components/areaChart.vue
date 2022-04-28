<template>
  <div id="chart" style="width: 100%">
    <apexchart
      type="area"
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
    let data = ref([
      {
        name: "Product",
        data: [10, 34, 67, 90, 86, 24, 69, 91, 148],
      },
      //   {
      //     name: "Desktops",
      //     data: [10, 41, 35, 51, 49, 62, 69, 91, 148],
      //   },
      //   {
      //     name: "Desktops",
      //     data: [10, 41, 35, 51, 49, 62, 69, 91, 148],
      //   },
      //   {
      //     name: "Desktops",
      //     data: [10, 41, 35, 51, 49, 62, 69, 91, 148],
      //   },
      //   {
      //     name: "Desktops",
      //     data: [10, 41, 35, 51, 49, 62, 69, 91, 148],
      //   },
      //   {
      //     name: "Desktops",
      //     data: [10, 41, 35, 51, 49, 62, 69, 91, 148],
      //   },
      //   {
      //     name: "Desktops",
      //     data: [10, 41, 35, 51, 49, 62, 69, 91, 148],
      //   },
      //   {
      //     name: "Desktops",
      //     data: [10, 41, 35, 51, 49, 62, 69, 91, 148],
      //   },
    ]);

    let option = ref({
      chart: {
        height: 350,
        type: "area",
      },
      dataLabels: {
        enabled: false,
      },
      markers: {
        size: 5,
      },
      stroke: {
        curve: "straight",
      },
      title: {
        text: "Area Chart",
        align: "left",
      },
      grid: {
        row: {
          colors: ["#f3f3f3", "transparent"], // takes an array which will be repeated on columns
          opacity: 0.5,
        },
      },
      xaxis: {
        categories: [
          "Jan",
          "Feb",
          "Mar",
          "Apr",
          "May",
          "Jun",
          "Jul",
          "Aug",
          "Sep",
        ],
      },
    });
    return { data, option };
  },
});
</script>
