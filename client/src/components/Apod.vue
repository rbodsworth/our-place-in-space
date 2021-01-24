<template>
  <div id='apod'>
    <date-form/>
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
import DateForm from './DateForm.vue';

export default {
    name: 'apod',
    components: {
      'date-form': DateForm
    },
    data () {
      return {
        picOfTheDay: undefined,
        selectedDate: undefined
      }
    },

    mounted () {
      this.getApod()
    },
    
    methods: {
        getApod: function(){
            fetch(`https://api.nasa.gov/planetary/apod?api_key=${APIkey}`)
            .then(res => res.json())
            .then(data => this.picOfTheDay = data)
            },
        
        getSelectedApod: function(){
          //take selected date off eventbus and update this.selectedDate
          // fetch data from api using selected date as a parameter
          // new request should return a json response that includes new image and assoc details
          
        }
  
    }

}
</script>

<style>


#apod {
  text-align: center;
}

</style>