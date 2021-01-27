<template>
  <div id=main>
    <apod></apod>
    <hr>
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
#main 
  { background-image: linear-gradient(to bottom, #002857, #1d1d1d 57%, #050505);

}

</style>