<template>
  <div>
    <!-- <apod></apod> -->
    <mars></mars>
  </div>
</template>

<script>
// import Apod from './components/Apod.vue';
import Mars from './components/Mars.vue';

export default {
  name: 'app',
  components: {
    // 'apod' : Apod,
    'mars' : Mars
  }
}
</script>

<style>
</style>