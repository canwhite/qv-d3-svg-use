<template>
  <Svg msg="Welcome to Your Vue.js App"/>
  <D3 msg="Welcome to Your Vue.js App"/>
</template>

<script>
import Svg from './components/Svg.vue'
import D3  from './components/D3.vue'

export default {
  name: 'App',
  components: {
    Svg ,
    D3
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
