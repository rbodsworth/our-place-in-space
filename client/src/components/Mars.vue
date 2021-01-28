<template>
<div id="marsmain">

  <h2 class="subtitle">Our closest neighbour is a frozen desert</h2>
  <h3>Today's photo from Mars</h3>

  <img class="mars-image" v-if="marsData" :src="marsData.photos[0].img_src">
  <img class="mars-image" v-else :src="marsPhotos[0].img_src">

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

import { APIkey } from '@/assets/MARS_API_KEY';
import { eventBus } from '../main.js';


export default {
  name: 'mars', 

  data() {
    return { 
      marsPhotos: [],
      datePicked: undefined,
      marsData: undefined,
      archiveMarsPhotos: []
      }
  },


  methods: {
    getPhotos: function(){
      fetch(`https://api.nasa.gov/mars-photos/api/v1/rovers/curiosity/latest_photos?api_key=${APIkey}&page=1`)
      .then( res => res.json())
      .then (data => this.marsPhotos = data.latest_photos)
    },

    createArchiveUrl: function() {
        return this.archiveUrl = `https://api.nasa.gov/mars-photos/api/v1/rovers/curiosity/photos?earth_date=${this.datePicked}&api_key=${APIkey}`;
      },

    mapImageUrls: function(data){
      this.archiveMarsPhotos.push('banana')
      // return data.map(obj => obj.photos.image_src)
      console.log('mars dat', data)
    }

  },

  mounted () {
  this.getPhotos()

  eventBus.$on("date-picked", (date) => {
    this.datePicked = date;
    fetch(this.createArchiveUrl())
    .then(res => res.json())
    .then(data => this.marsData = data)
    }) 
  },
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

</style>