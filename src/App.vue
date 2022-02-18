<template>
  <div id="app">
    <div id="nav">
      <h3>Line chart with a single dataset.....</h3>
      <LineChart/>
      <h3>Dynamic chart with a multiple datasets.....</h3>
      <ContainerComp/>
    </div>
  </div>
</template>

<script>
import LineChart from './components/LineChart.vue'
import ContainerComp from './components/container.vue'

export default {
  components:{
    LineChart,
    ContainerComp
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: black;
}
</style>