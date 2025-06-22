<template>
  <div class="app">
    <h1>Hello Vue!</h1>
    <AgoraDemo />
  </div>
</template>

<script>
import AgoraDemo from './components/AgoraDemo.vue'

export default {
  name: 'App',
  components: {
    AgoraDemo
  }
}
</script>

<style>
.app {
  font-family: Arial, sans-serif;
  padding: 1em;
}
</style>
