<template>
  <v-container>
    <v-row v-for="link of links" :key="link.href" justify="center">
      <v-col cols="auto">
        <v-btn :to="link.href" solo color="orange">{{ link.name }}</v-btn>
      </v-col>
    </v-row>
  </v-container>
</template>

<script setup>
const links = [
  { href: "/plotly", name: "Plotly.js" },
  { href: "/apex", name: "Apexcharts" },
  { href: "/echarts", name: "Echarts" },
];
</script>
