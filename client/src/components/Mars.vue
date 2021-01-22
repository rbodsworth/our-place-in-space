<template>
<div>
  <h1>test</h1>
<mars-photo-item v-for="(photo, index) in marsPhotos" :key="index" :photo="photo"/>

{{marsPhotos.latest_photos}}

</div>

</template>

<script>



import { APIkey } from '@/assets/MARS_API_KEY'
import MarsPhotoItem from './MarsPhotoItem.vue'

export default {
  components: { 
    'mars-photo-item': MarsPhotoItem
  
  },

  name: 'mars', 
  data() {
    return {
    marsPhotos: []
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
  }

}
</script>

<style>

</style>