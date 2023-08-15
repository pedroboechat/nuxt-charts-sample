<template>
  <v-container>
    <v-row>
      <v-col>
        <h1>Plotly sample</h1>
      </v-col>
    </v-row>
    <v-row>
      <v-col>
        <div id="plot"></div>
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

<script setup>
const { $Plotly } = useNuxtApp();

const plotData = ref(
  Array.from({ length: 10 }, () => Math.floor(Math.random() * 100))
);
const plotCategories = ref(
  Array.from({ length: 10 }, (_, i) => new Date().getFullYear() - 9 + i)
);
const lastClick = ref("---");

function handlePlotlyClick(event) {
  console.log(event);
  // lastClick.value = `${plotCategories.value[
  //   config.dataPointIndex
  // ].toString()} -> ${plotData.value[config.dataPointIndex].toString()}`;
}

function plotGraph() {
  if (process.client) {
    $Plotly.newPlot("plot", {
      data: [
        {
          x: plotCategories.value,
          y: plotData.value,
          type: "bar",
        },
      ],
    });
  }
}

const updateChart = () => {
  // generate array of random numbers of length 10
  plotData.value = Array.from({ length: 10 }, () =>
    Math.floor(Math.random() * 100)
  );

  plotGraph();
};

onMounted(async () => {
  // Create plots
  await nextTick();
  plotGraph();
});
</script>
