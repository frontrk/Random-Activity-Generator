<template>
  <div id="app">    
    <Box msg="Random Activity Generator"/>
  </div>
</template>

<script>
import Box from './components/Box.vue'

export default {
  name: 'app',
  components: {
    Box    
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
