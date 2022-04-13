<template>
  <Container msg="Welcome to Your Vue.js App"/>
</template>

<script>
import Container from './components/container.vue'

export default {
  name: 'App',
  components: {
    Container
  }
}
</script>

<style>
html,body,#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  margin: 0;
  padding: 0;
  height: 100%;
  overflow: hidden;
}
</style>
