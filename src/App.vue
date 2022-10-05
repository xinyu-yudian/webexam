<template>
  <div id="app">
    <HelloWorld/>
    <Cesium/>
  </div>
  
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import Cesium from './components/Cesium.vue'

export default {
  name: 'App',
  components: {
    HelloWorld,
    Cesium
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
  margin-top: 60px;
}
</style>
