<template>
  <div id='apod'>
      <h2>Picture of the day</h2>
      <h3> {{picOfTheDay.title}} </h3>
      <img :src="picOfTheDay.url" width='500'>
      <p> Copyright: {{picOfTheDay.copyright}} </p>

      <h2>Explanation</h2>
      <p> {{picOfTheDay.explanation}}</p>

      <h2>Date</h2>
      <p> {{picOfTheDay.date}}</p>
  </div>
</template>

<script>
import { APIkey } from '../assets/APOD-API-Key';

export default {
    name: 'apod',
    data () {
      return {
        picOfTheDay: undefined
      }
    }
    ,

    mounted () {
      this.getApod()
    },
    
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


#apod {
  text-align: center;
}

</style>