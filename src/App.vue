<template>
  <div id="app">
  <trellomain />
  </div>
</template>

<script>

import trellomain from './components/trelloCards/trelloCards.main.vue'
export default {
  name: 'App',
  components: {
     trellomain
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  /* margin-top: 60px; */
}
</style>
