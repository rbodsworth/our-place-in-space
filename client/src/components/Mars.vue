<template>
<div id="mars">
   <!-- <mars-date-item ></mars-date-item> -->
   <!-- <mars-date-item v-for="(photos, index) in datePic" :key="index" :photos="photos"  /> -->

  <h1>Mars Rover Photos</h1>
  <p>Image data gathered by NASA's Curiosity, Opportunity, and Spirit rovers on Mars</p>
<mars-date-item ></mars-date-item>
<mars-photo-item v-for="(photo, index) in marsPhotos" :key="index" :photo="photo"/>

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
    datePic: [],
    selectedDateForAll: null
    }
  },

  mounted () {
    this.getPhotos()

    //  eventBus.$on('selected-date', (datePic) => {
    //   this.datePic = datePic
 
    eventBus.$on("date-test", (payload) => this.selectedDateForAll = payload)

      
    },

  methods: {
    getPhotos: function(){
      fetch(`https://api.nasa.gov/mars-photos/api/v1/rovers/curiosity/latest_photos?api_key=${APIkey}&page=0`)
      .then( res => res.json())
      .then (data => this.marsPhotos = data.latest_photos)

      
    }


  
  }

}
</script>

<style>
#mars {
  text-align: center;
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
}

</style>