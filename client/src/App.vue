<template>

  <div id=main>
    <h2>Astronomy Picture Of the Day</h2>
    <apod></apod>
    <hr>
    <h2>Mars Rover Photos</h2>
    <mars></mars>
    <epic-image/>
  </div>
</template>

<script>

import EPIC from './components/EPIC';
import Mars from './components/Mars.vue';
import Apod from './components/Apod.vue';
import DateForm from './components/DateForm.vue';

export default {
  name: 'app',
  components: {
    'mars' : Mars,
    "epic-image": EPIC,
    'apod' : Apod,
    'date-form' : DateForm
  },
}

</script>

<style>


.date {
  margin: 20px;
  
}


#main {
  background-color: #140057;
  background-image: url("https://www.transparenttextures.com/patterns/asfalt-light.png");
  color: white;
  text-align: center;
  padding: 50px;
  font-family: 'Roboto', sans-serif;
}

</style>