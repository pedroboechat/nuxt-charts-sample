<template>
  <v-container>
    <v-row>
      <v-col>
        <h1>Apexchart sample</h1>
      </v-col>
    </v-row>
    <v-row>
      <v-col>
        <ClientOnly>
          <apexchart
            :key="series"
            height="400"
            width="100%"
            :options="options"
            :series="series"
            @data-point-selection="handleDataPointSelection"
          ></apexchart>
        </ClientOnly>
      </v-col>
    </v-row>
    <v-row justify="center">
      <v-col cols="auto">
        <v-btn color="blue" @click="updateChart"> Change </v-btn>
      </v-col>
    </v-row>
    <v-row justify="center">
      <v-col cols="auto">
        <h1>Last click: {{ lastClick }}</h1>
      </v-col>
    </v-row>
  </v-container>
</template>

<script setup lang="ts">
const plotData = ref(
  Array.from({ length: 10 }, () => Math.floor(Math.random() * 100))
);
const plotCategories = ref(
  Array.from({ length: 10 }, (_, i) => new Date().getFullYear() - 9 + i)
);
const lastClick = ref("---");

function handleDataPointSelection(event, chartContext, config) {
  console.log(chartContext, config);
  lastClick.value = `${plotCategories.value[
    config.dataPointIndex
  ].toString()} -> ${plotData.value[config.dataPointIndex].toString()}`;
}

const options = ref({
  chart: {
    type: "bar",
  },
  plotOptions: {},
});
const series = ref([
  {
    name: "Score",
    data: [],
  },
]);
const updateChart = () => {
  // generate array of random numbers of length 10
  plotData.value = Array.from({ length: 10 }, () =>
    Math.floor(Math.random() * 100)
  );

  options.value = {
    ...options.value,
    xaxis: {
      categories: plotCategories, // array of last 10 years
    },
  };
  series.value = [
    {
      name: "Score",
      data: plotData.value,
    },
  ];
};

onMounted(() => {
  updateChart();
});
</script>
