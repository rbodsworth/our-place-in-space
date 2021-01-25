<template>
<div id="mars">
  <h1>Mars Rover Photos</h1>
  <p>Image data gathered by NASA's Curiosity, Opportunity, and Spirit rovers on Mars</p>
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
    datePic: undefined
    }
  },

  mounted () {
    this.getPhotos()
  },

  methods: {
    getPhotos: function(){
      fetch(`https://api.nasa.gov/mars-photos/api/v1/rovers/curiosity/latest_photos?api_key=${APIkey}`)
      .then( res => res.json())
      .then (data => this.marsPhotos = data.latest_photos)
    },

  computed: {
    newPic() {eventBus.$on("selected-date", (datePic) =>{
        this.datePic = datePic
  })}}
  
  }

}
</script>

<style>
#mars {
  text-align: center;
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
}

</style>