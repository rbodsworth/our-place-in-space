<template>
  <div>
    <mars></mars>
    <apod></apod>
  </div>
</template>

<script>

import Mars from './components/Mars.vue';
import Apod from './components/Apod.vue';

export default {
  name: 'app',
  components: {
    // 'apod' : Apod,
    'mars' : Mars,
    'apod' : Apod
  }
}

</script>

<style>

</style>