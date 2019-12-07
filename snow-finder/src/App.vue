<template>
  <v-app>
    <img src="./assets/title.png">
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
<style scoped>
img {
  width: 300px;
  height: 150px;
}
</style>
