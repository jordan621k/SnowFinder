<template>
  <v-app>
      <Stats />
  </v-app>
</template>

<script>
import Stats from './components/Stats';

export default {
  name: 'App',

  components: {
    Stats,
  },

  data: () => ({
  }),
};
</script>
