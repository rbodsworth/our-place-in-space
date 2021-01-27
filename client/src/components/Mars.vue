<template>
<div id = "marsmain">
  <h3>Image data gathered by NASA's Curiosity, Opportunity, and Spirit rovers on Mars</h3>
  <mars-date-item ></mars-date-item>

  <img :src="marsPhotos[0].img_src" width="800">
  <div id="marscap">
  
  <p class="marscaption">Earth date: {{marsPhotos[0].earth_date}}
  Mars sol: {{marsPhotos[0].sol}}
  Rover name: {{marsPhotos[0].rover.name}}</p>
  </div>

</div>


</template>

<script>

import { APIkey } from '@/assets/MARS_API_KEY'
import MarsPhotoItem from './MarsPhotoItem.vue'
import MarsDateItem from './MarsDateItem.vue'
import { eventBus } from '../main.js';


export default {
  components: { 
    'mars-photo-item': MarsPhotoItem, 
    'mars-date-item': MarsDateItem
  
  },

  name: 'mars', 
  data() {
    return {
    marsPhotos: [],
    }
  },

  mounted () {
    this.getPhotos()
    
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

/* #heads {
  text-align: center;
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
} */


</style>