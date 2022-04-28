<template>
  <div>
    <draggable
      class="grid"
      v-model="myArray"
      group="people"
      @start="drag = true"
      @end="drag = false"
      item-key="id"
    >
      <template #item="{ element }">
        <div>
          <CandleStickChart v-if="element === 'candleStickChart'" />
          <BarChart v-if="element === 'bar'" />
          <LineChart v-if="element === 'line'" />
          <StackedBarChart v-if="element === 'stackedbarchart'" />
          <AreaChart v-if="element === 'areachart'" />
          <Pie v-if="element === 'pie'" />
          <DoughnutChart v-if="element === 'doughnut'" />
          <StackedBarLine v-if="element === 'stackedlinebarchart'" />
        </div>
      </template>
    </draggable>
  </div>
</template>
<script lang="ts">
import { defineComponent, ref } from "vue";
import draggable from "vuedraggable";
import CandleStickChart from "@/components/candleStickChart.vue";
import BarChart from "@/components/barChart.vue";
import LineChart from "@/components/lineChart.vue";
import StackedBarChart from "@/components/barStackedChart.vue";
import AreaChart from "@/components/areaChart.vue";
import Pie from "@/components/pieChart.vue";
import DoughnutChart from "@/components/doughnutChart.vue";
import StackedBarLine from "@/components/stackedlinebarchart.vue";

export default defineComponent({
  components: {
    draggable,
    CandleStickChart,
    BarChart,
    LineChart,
    StackedBarChart,
    AreaChart,
    Pie,
    DoughnutChart,
    StackedBarLine,
  },
  setup() {
    let drag = ref(false);
    let myArray = ref([
      "candleStickChart",
      "bar",
      "line",
      "stackedbarchart",
      "areachart",
      "pie",
      "doughnut",
      "stackedlinebarchart",
    ]);
    return { drag, myArray };
  },
});
</script>
<style scoped>
.grid {
  display: grid;
  grid-template-columns: repeat(3, 500px);
}
</style>
