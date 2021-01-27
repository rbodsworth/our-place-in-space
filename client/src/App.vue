<template>

  <div id="main">
    <h1 class="title">Our Place in Space</h1>
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



h1, h2, h3, h4, h5, h6 {
    font-family: Helvetica, Arial, sans-serif ;
    text-transform: uppercase;
    text-align: left;
    max-width: 800px;
}

p {
  font-family: Georgia, 'Times New Roman', Times, serif;
  font-size: 20px;
  line-height: 1.46;
  text-align: left;
  max-width: 800px;
}

img { width: 100%; }

body { margin: 0px }

#main {
  display: flex;
  flex-direction: column;
  background-image: linear-gradient(to bottom, #002857, #1d1d1d 57%, #050505);

  /* background-color: #140057; */
  /* background-image: url("https://www.transparenttextures.com/patterns/asfalt-light.png"); */
  color: white;
  text-align: center;
  padding: 15px;
  /* font-family: 'Roboto', sans-serif; */
}

.date {
  margin: 20px;  
}

.date-input { margin-left:auto; }

.title {
  font-family: Georgia, 'Times New Roman', Times, serif;
  font-size: 40px;
  text-transform:capitalize;
  /* align-self: left; */
  margin-right: auto;
}

.title-block {
  display: flex;
}

.date-right {
  margin-left: auto;
  font-weight: 100;
}

.subtitle {
  font-family: Georgia, 'Times New Roman', Times, serif;
  font-weight: 100;
  font-style: italic;
  text-transform: initial;
}

</style>