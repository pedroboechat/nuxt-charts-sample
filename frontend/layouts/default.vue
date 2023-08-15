<template>
  <v-layout>
    <v-app-bar :elevation="1">
      <template #prepend>
        <nuxt-link to="/">
          <v-icon color="black">mdi-home</v-icon>
        </nuxt-link>
      </template>
      <template #append>
        <v-list v-for="navItem in navigation" :key="navItem.title" nav>
          <v-list-item
            active-class="navbar-active-link"
            :title="navItem.title"
            :to="navItem.href"
            :ripple="false"
            variant="plain"
          ></v-list-item>
        </v-list>
      </template>
    </v-app-bar>

    <v-main>
      <slot></slot>
    </v-main>

    <v-footer app border>
      This is a footer! @ {{ new Date().getFullYear() }}
    </v-footer>
  </v-layout>
</template>

<script setup>
const navigation = ref([]);
</script>
