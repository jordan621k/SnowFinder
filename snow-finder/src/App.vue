<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <Stats />
  </div>
</template>

<script>
import Stats from './components/Stats.vue'

export default {
  name: 'app',
  components: {
    Stats
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
