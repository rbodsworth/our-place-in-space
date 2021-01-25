<template>
<div>
  <input id="date" type="date">
  <button id="button" href="">Submit</button>
  </div>
</template>

<script>

import { APIkey } from '@/assets/MARS_API_KEY'

export default {
    name: 'mars-date-item',
    data () {
        return {
            selected_date: null 

        }
    },

    methods: {
      getPhotos: function(){
      fetch(`https://api.nasa.gov/mars-photos/api/v1/rovers/curiosity/photos?earth_date=${date}&api_key=${APIkey}`)
      .then( res => res.json())
      .then(data => )

}}}


</script>

<style>

</style>