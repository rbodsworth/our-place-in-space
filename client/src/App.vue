<template>
  <div id=main>
    <h2>Astronomy Picture Of the Day</h2>
    <apod></apod>
    <hr>
    <h2>Mars Rover Photos</h2>
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


.date {
  margin: 20px;
  
}

/* .submit {
  font-family: Helvetica;
  font-weight: bold;
  font-stretch: normal;
  font-style: normal;
  line-height: normal;
  letter-spacing: 0.58px;
  color: #FFFFFF;
  background-color: #006DFF;
  border-radius: 26px;
  padding: 10px 10px;
  width: 115px;
  height: 39px;
} */

/* .submit {

} */



#main {
  background-color: darkblue;
  color: white;
  text-align: center;
  padding: 50px;
}

</style>