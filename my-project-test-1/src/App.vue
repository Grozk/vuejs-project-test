<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <JoinParty msg="Jo & Sy"/>
  </div>
</template>

<script>
import JoinParty from './components/JoinParty.vue'

export default {
  name: 'app',
  components: {
    JoinParty
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
