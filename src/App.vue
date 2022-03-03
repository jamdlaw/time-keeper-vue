<template>
  <img alt="Vue logo" src="./assets/logo.png">
  <Timer time_to_complete="30"/>
  <Message inputMsg = 'test'/>
</template>

<script>
import Timer from './components/Timer.vue'
import Message from './components/Message.vue'

export default {
  name: 'App',
  components: {
    Timer,
    Message
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
