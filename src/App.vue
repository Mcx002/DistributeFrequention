<template>
  <div id="app">
    <DistributeFrequestion />
  </div>
</template>

<script>
import DistributeFrequestion from './components/DistributeFrequention.vue'

export default {
  name: 'App',
  components: {
    DistributeFrequestion
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
