<template>
  <div id="app">
    <mars></mars>
    <epic-image/>
  <div>
</template>

<script>

import EPIC from './components/EPIC';
import Mars from './components/Mars.vue';
// import Apod from './components/Apod.vue';

export default {
  name: 'app',
  components: {
    'mars' : Mars,
    "epic-image": EPIC
    // 'apod' : Apod
  }
}

</script>

<style>

</style>