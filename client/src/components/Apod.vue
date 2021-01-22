<template>
  <div>
      <h1>Picture of the day</h1>
      <p> {{picOfTheDay.explanation}}</p>
  </div>
</template>

<script>
import { APIkey } from '../assets/APOD-API-Key';

export default {
    name: 'apod',
    data () {
      return {
        picOfTheDay = undefined
      }
    }
    ,
    methods: {
        getApod: function(){
            fetch('https://api.nasa.gov/planetary/apod?api_key=DEMO_KEY')
            .then(res => res.json())
            .then(data => this.picOfTheDay = data)
            },
    }

}
</script>

<style>

</style>