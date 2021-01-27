<template>
<div id="marsmain">
  <h2 class="subtitle">Our closest neighbour is a frozen desert</h2>
  <h3>Today's photo from Mars</h3>
  <!-- <mars-date-item class="date-input"></mars-date-item> -->
  <!-- <date-item class="date-input"/> -->

  <img class="mars-image" v-if="marsPhotos" :src="marsPhotos[0].img_src">

  <div id="marscap">
    <span class="marscaption">Date: <strong>{{marsPhotos[0].earth_date}}</strong></span>
    <span>Sol: <strong>{{marsPhotos[0].sol}}</strong></span>
    <span>Name: <strong>{{marsPhotos[0].rover.name}}</strong></span>
    <span>Launch date: <strong>{{marsPhotos[0].rover.launch_date}}</strong></span>
    <span>Landing date: <strong>{{marsPhotos[0].rover.landing_date}}</strong></span>
    <span>Status: <strong>{{marsPhotos[0].rover.status}}</strong></span>
  </div>

</div>

</template>


<script>

import { APIkey } from '@/assets/MARS_API_KEY'
import MarsPhotoItem from './MarsPhotoItem.vue'
// import MarsDateItem from './MarsDateItem.vue'
import { eventBus } from '../main.js';
import DateForm from './DateForm.vue';


export default {
  components: { 
    'mars-photo-item': MarsPhotoItem, 
    // 'mars-date-item': MarsDateItem
    "date-item": DateForm
  
  },
  
  name: 'mars', 

  data() {
    return {
      marsPhotos: [],
    }
  },

  mounted() {
    this.getPhotos()
    // eventBus.$on('selected-date', (payload) => this.marsPhotos = payload)
    eventBus.$on('date-selected', (payload) => this.marsPhotos = payload)
  },

  methods: {
    getPhotos: function(){
      fetch(`https://api.nasa.gov/mars-photos/api/v1/rovers/curiosity/latest_photos?api_key=${APIkey}&page=1`)
      .then( res => res.json())
      .then (data => this.marsPhotos = data.latest_photos)
    },
  }
}

</script>

<style>

#marsmain {
  display: flex;
  flex-direction: column;
}

#marscap {
  margin-top: 15px;
  margin-left: auto;
}

#marscap > span {
  margin-left: 10px;
  text-transform: uppercase;
  font-family: Helvetica, Arial, sans-serif;
  font-size: 12px;
}
 /* .mars-image {
  width: 50%;
  height: 50%;
  max-width: 1000px;
  max-height: 1000px;
} */



</style>