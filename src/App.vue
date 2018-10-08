<template>
  <div id="app">
    <Memory msg="Memory"/>
  </div>
</template>

<script>
import Memory from './components/Memory.vue'

export default {
  name: 'app',
  components: {
    Memory
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
