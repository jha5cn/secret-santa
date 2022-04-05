<template>
  <div id="app">
    <img src="./assets/santa.jpg" alt="Santa!"
    contain  
    height="300px"
    width="200px">
    <SecretSanta msg="Secret Santa"/>
  </div>
</template>

<script>
import SecretSanta from './components/SecretSanta.vue'

export default {
  name: 'App',
  components: {
    SecretSanta
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
