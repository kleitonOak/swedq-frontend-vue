<template>
  <div id="app">
    <VehicleStatus msg="Welcome Vehicle Status App"/>
  </div>
</template>

<script>
import VehicleStatus from './components/VehicleStatus.vue'

export default {
  name: 'app',
  components: {
    VehicleStatus
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
