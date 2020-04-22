<template>
  <div id="app">
    <CovidDetail/>
  </div>
</template>

<script>
import CovidDetail from './components/CovidDetail.vue'

export default {
  name: 'App',
  components: {
    CovidDetail
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
}
body{
  background-color:#5594f7;
}
</style>
