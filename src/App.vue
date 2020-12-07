<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <UploadPhoto msg="Welcome to Your Vue.js App"/>
    <HttpRequest msg="Welcome to Your Vue.js App"/>
  </div>
</template>

<script>
import UploadPhoto from './components/UploadPhoto.vue'
import HttpRequest from './components/HttpRequest.vue'

export default {
  name: 'App',
  components: {
    UploadPhoto,
    HttpRequest
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
