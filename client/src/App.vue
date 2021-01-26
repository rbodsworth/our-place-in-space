<template>
  <div id="app">
    <epic-image/>
  </div>
</template>

<script>
import EPIC from './components/EPIC'

export default {
  name: 'App',
  components: {
    "epic-image": EPIC
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
