<template>
  <div class="container">
    <div id="chart" style="width: 100%">
      <apexchart
        type="candlestick"
        height="350"
        :options="chartOptions"
        :series="series"
      ></apexchart>
    </div>
    <div style="width: 100%">
      <BarChart v-bind="barChartProps" />
    </div>
    <div style="width: 100%">
      <LineChart />
    </div>
    <div>
      <PieChart :chartData="pieChartData" />
    </div>
    <div>
      <PieChart v-bind="pieChartProps" />
    </div>
    <div>
      <DoughnutChart v-bind="doughnutChartProps" />
    </div>
  </div>
</template>
<script lang="ts">
import { Chart, registerables, ChartData, ChartOptions } from "chart.js";
import { defineComponent, ref, reactive, computed } from "vue";
import {
  useBarChart,
  BarChart,
  PieChart,
  usePieChart,
  DoughnutChart,
  useDoughnutChart,
} from "vue-chart-3";
import VueApexCharts from "vue3-apexcharts";
import LineChart from "./polararea.vue";

Chart.register(...registerables);
export default defineComponent({
  components: {
    apexchart: VueApexCharts,
    BarChart,
    LineChart,
    PieChart,
    DoughnutChart,
  },
  setup() {
    const dataValues = ref([30, 40, 60, 70, 5, 10, 60]);
    const dataLabels = ref([
      "monday",
      "tuesday",
      "wednesday",
      "thursday",
      "friday",
      "saturday",
      "sunday",
    ]);
    const toggleLegend = ref(true);

    const testData = computed<ChartData<"doughnut">>(() => ({
      labels: dataLabels.value,
      datasets: [
        {
          data: dataValues.value,
          backgroundColor: [
            "#77CEFF",
            "#0079AF",
            "#123E6B",
            "#97B0C4",
            "#A5C8ED",
          ],
        },
      ],
    }));

    const bardata = computed<ChartData<"bar">>(() => ({
      labels: dataLabels.value,
      datasets: [
        {
          label: "Stocks",
          data: [12, 34, 45, 67, 23, 98, 34],

          backgroundColor: "#77CEFF",
        },
        {
          label: "stock 2",
          data: [22, 43, 15, 57, 73, 28, 34],
          backgroundColor: "#0079AF",
        },
        {
          label: "stock 3",
          data: [20, 49, 75, 97, 23, 98, 34],
          backgroundColor: "#97B0C4",
        },
      ],
    }));

    const barOptions = computed<ChartOptions<"bar">>(() => ({
      scales: {
        x: {
          stacked: true,
        },
        y: {
          stacked: true,
        },
      },
    }));

    const { barChartProps, barChartRef } = useBarChart({
      chartData: bardata,
      options: barOptions,
    });

    const Doptions = computed<ChartOptions<"doughnut">>(() => ({
      scales: {
        myScale: {
          type: "logarithmic",
          position: toggleLegend.value ? "left" : "right",
        },
      },
      plugins: {
        legend: {
          position: toggleLegend.value ? "top" : "bottom",
        },
        title: {
          display: true,
          text: "Chart.js Doughnut Chart",
        },
      },
    }));

    const { doughnutChartProps, doughnutChartRef } = useDoughnutChart({
      chartData: testData,
      options: Doptions,
    });

    const pieSeriesChartData = computed<ChartData<"pie">>(() => ({
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
          backgroundColor: ["#AAA", "#777"],
          data: [21, 79],
        },
        {
          backgroundColor: ["hsl(0, 100%, 60%)", "hsl(0, 100%, 35%)"],
          data: [33, 67],
        },
        {
          backgroundColor: ["hsl(100, 100%, 60%)", "hsl(100, 100%, 35%)"],
          data: [20, 80],
        },
        {
          backgroundColor: ["hsl(180, 100%, 60%)", "hsl(180, 100%, 35%)"],
          data: [10, 90],
        },
      ],
    }));

    const options = computed<ChartOptions<"pie">>(() => ({
      plugins: {
        legend: {
          labels: {
            generateLabels: function (chart: any) {
              console.log("hererreer", chart);
              const original =
                Chart.overrides.pie.plugins.legend.labels.generateLabels;
              const labelsOriginal = original.call(this, chart);

              let datasetColors = chart.data.datasets.map(function (e: any) {
                return e.backgroundColor;
              });
              datasetColors = datasetColors.flat();
              labelsOriginal.forEach((label: any) => {
                // There are twice as many labels as there are datasets. This converts the label index into the corresponding dataset index
                label.datasetIndex = (label.index - (label.index % 2)) / 2;

                // The hidden state must match the dataset's hidden state
                label.hidden = !chart.isDatasetVisible(label.datasetIndex);

                // Change the color to match the dataset
                label.fillStyle = datasetColors[label.index];
              });
              return labelsOriginal;
            },
          },
        },

        // title: {
        //   display: true,
        //   text: "Chart.js Doughnut Chart",
        // },
      },
    }));

    // const seriesOptions = reactive({
    //   responsive: true,
    //   plugins: {
    //     legend: {
    //       lables: {
    //         generateLabels: function (Chart: any) {
    //           // Get the default label list
    //           console.log("abc", Chart);
    //           const original =
    //             Chart.overrides.pie.plugins.legend.labels.generateLabels;
    //           const labelsOriginal = original.call(this, Chart);

    //           // Build an array of colors used in the datasets of the Chart
    //           let datasetColors = Chart.data.datasets.map(function (e: any) {
    //             console.log(e);
    //             return e.backgroundColor;
    //           });
    //           datasetColors = datasetColors.flat();

    //           // Modify the color and hide state of each label
    //           labelsOriginal.forEach((label: any) => {
    //             // There are twice as many labels as there are datasets. This converts the label index into the corresponding dataset index
    //             label.datasetIndex = (label.index - (label.index % 2)) / 2;

    //             // The hidden state must match the dataset's hidden state
    //             label.hidden = !Chart.isDatasetVisible(label.datasetIndex);

    //             // Change the color to match the dataset
    //             label.fillStyle = datasetColors[label.index];
    //           });

    //           return labelsOriginal;
    //         },
    //       },
    //     },
    //   },
    // });

    const { pieChartProps, pieChartRef } = usePieChart({
      chartData: pieSeriesChartData,
      options,
    });

    const pieChartData = reactive({
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
        },
        {
          label: "stock 2",
          data: [22, 43, 15, 57, 73, 28, 34],
          backgroundColor: "#0079AF",
        },
        {
          label: "stock 3",
          data: [20, 49, 75, 97, 23, 98, 34],
          backgroundColor: "#97B0C4",
        },
      ],
    });

    const barChartData = reactive({
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
        },
        {
          label: "stock 2",
          data: [22, 43, 15, 57, 73, 28, 34],
          backgroundColor: "#0079AF",
        },
        {
          label: "stock 3",
          data: [20, 49, 75, 97, 23, 98, 34],
          backgroundColor: "#97B0C4",
        },
      ],
    });

    const dataoptions = ref({
      scales: {
        x: {
          stacked: true,
        },
        y: {
          stacked: true,
        },
      },
    });

    const pieOptions = ref({
      scales: {
        x: {
          stacked: true,
        },
        y: {
          stacked: true,
        },
      },
    });

    let series = ref([
      {
        data: [
          {
            x: new Date(1538778600000),
            y: [6629.81, 6650.5, 6623.04, 6633.33],
          },
          {
            x: new Date(1538780400000),
            y: [6632.01, 6643.59, 6620, 6630.11],
          },
          {
            x: new Date(1538782200000),
            y: [6630.71, 6648.95, 6623.34, 6635.65],
          },
          {
            x: new Date(1538784000000),
            y: [6635.65, 6651, 6629.67, 6638.24],
          },
          {
            x: new Date(1538785800000),
            y: [6638.24, 6640, 6620, 6624.47],
          },
          {
            x: new Date(1538787600000),
            y: [6624.53, 6636.03, 6621.68, 6624.31],
          },
          {
            x: new Date(1538789400000),
            y: [6624.61, 6632.2, 6617, 6626.02],
          },
          {
            x: new Date(1538791200000),
            y: [6627, 6627.62, 6584.22, 6603.02],
          },
          {
            x: new Date(1538793000000),
            y: [6605, 6608.03, 6598.95, 6604.01],
          },
          {
            x: new Date(1538794800000),
            y: [6604.5, 6614.4, 6602.26, 6608.02],
          },
          {
            x: new Date(1538796600000),
            y: [6608.02, 6610.68, 6601.99, 6608.91],
          },
          {
            x: new Date(1538798400000),
            y: [6608.91, 6618.99, 6608.01, 6612],
          },
          {
            x: new Date(1538800200000),
            y: [6612, 6615.13, 6605.09, 6612],
          },
          {
            x: new Date(1538802000000),
            y: [6612, 6624.12, 6608.43, 6622.95],
          },
          {
            x: new Date(1538803800000),
            y: [6623.91, 6623.91, 6615, 6615.67],
          },
          {
            x: new Date(1538805600000),
            y: [6618.69, 6618.74, 6610, 6610.4],
          },
          {
            x: new Date(1538807400000),
            y: [6611, 6622.78, 6610.4, 6614.9],
          },
          {
            x: new Date(1538809200000),
            y: [6614.9, 6626.2, 6613.33, 6623.45],
          },
          {
            x: new Date(1538811000000),
            y: [6623.48, 6627, 6618.38, 6620.35],
          },
          {
            x: new Date(1538812800000),
            y: [6619.43, 6620.35, 6610.05, 6615.53],
          },
          {
            x: new Date(1538814600000),
            y: [6615.53, 6617.93, 6610, 6615.19],
          },
          {
            x: new Date(1538816400000),
            y: [6615.19, 6621.6, 6608.2, 6620],
          },
          {
            x: new Date(1538818200000),
            y: [6619.54, 6625.17, 6614.15, 6620],
          },
          {
            x: new Date(1538820000000),
            y: [6620.33, 6634.15, 6617.24, 6624.61],
          },
          {
            x: new Date(1538821800000),
            y: [6625.95, 6626, 6611.66, 6617.58],
          },
          {
            x: new Date(1538823600000),
            y: [6619, 6625.97, 6595.27, 6598.86],
          },
          {
            x: new Date(1538825400000),
            y: [6598.86, 6598.88, 6570, 6587.16],
          },
          {
            x: new Date(1538827200000),
            y: [6588.86, 6600, 6580, 6593.4],
          },
        ],
      },
    ]);
    let chartOptions = ref({
      chart: {
        type: "candlestick",
        height: 350,
      },
      title: {
        text: "CandleStick Chart",
        align: "left",
      },
      xaxis: {
        type: "datetime",
      },
      yaxis: {
        tooltip: {
          enabled: true,
        },
      },
    });
    return {
      series,
      chartOptions,
      barChartData,
      dataoptions,
      pieChartData,
      pieOptions,
      pieChartRef,
      pieChartProps,
      doughnutChartRef,
      doughnutChartProps,
      barChartProps,
      barChartRef,
    };
  },
});
</script>
<style scoped>
.container {
  display: flex;
  width: 100%;
  justify-content: space-between;
  flex-wrap: wrap;
}
</style>
