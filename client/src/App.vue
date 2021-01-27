<template>
  <div>
    <apod></apod>
    <mars></mars>
  </div>
</template>

<script>

import Mars from './components/Mars.vue';
import Apod from './components/Apod.vue';
import DateForm from './components/DateForm.vue';

export default {
  name: 'app',
  components: {
    'mars' : Mars,
    'apod' : Apod,
    'date-form' : DateForm
  },
}

</script>

<style>

</style>