<template>
  <div id="app">
    <TRTC/>
  </div>
</template>

<script>
import TRTC from './components/TRTC.vue'

export default {
  name: 'App',
  components: {
    TRTC
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
