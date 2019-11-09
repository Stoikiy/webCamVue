<template>
  <div id="app">
    <WebCam/>
  </div>
</template>

<script>
import WebCam from "@/components/WebCam";

export default {
  name: 'app',
  components: { WebCam }
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
