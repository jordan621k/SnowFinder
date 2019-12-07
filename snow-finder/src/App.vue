<template>
  <v-app>
      <Stats />
      <Map />
  </v-app>
</template>

<script>
import Stats from './components/Stats';
import Map from './components/Map';
export default {
  name: 'App',

  components: {
    Stats,
    Map
  },

  data: () => ({
  }),
};
</script>
