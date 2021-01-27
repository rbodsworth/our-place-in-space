<template>
  <div id='apod'>
    <date-form></date-form>
      <h3> Date: {{picOfTheDay.date}}</h3>
      
      <h2>Picture of the day</h2>
      <h3> {{picOfTheDay.title}} </h3>
      <img :src="picOfTheDay.url" width='500'>
      <p> Copyright: {{picOfTheDay.copyright}} </p>

      <h2>Explanation</h2>
      <p> {{picOfTheDay.explanation}}</p>

  </div>
</template>

<script>
import { APIkey } from '../assets/APOD-API-Key';
import { eventBus } from '../main.js';
import DateForm from './DateForm.vue';

export default {
    name: 'apod',
    components: {
      'date-form': DateForm
    },
    data () {
      return {
        picOfTheDay: undefined
      }
    },

    mounted () {
      this.getApod()

      eventBus.$on("date-selected", (payload) => this.picOfTheDay = payload)

    },
    
    methods: {
        getApod: function(){
            fetch(`https://api.nasa.gov/planetary/apod?api_key=${APIkey}`)
            .then(res => res.json())
            .then(data => this.picOfTheDay = data)
            
            },
      
      
      
    }
}
        


    // EVERYTHING BELOW IS OUTSIDE OF OUR EXPORT DEFAULT()
    // computed: {
      
      // updateDate: function(){
      //   eventBus.$on("date-selected",  (date_selected_form) => {
      //     return payload = this.dateSelected;
      //   }) 
      // }
    // }

    // updatedPic() {
      //   eventBus.$on("selected-date", (picOfTheDate) => this.picOfTheDay = picOfTheDate)}
        
      // getUpdatedPic: function(`https://api.nasa.gov/planetary/apod?api_key=${APIkey}&date=${this.dateSelected}`)
      //       .then ( res => res.json())
      //       .then (data => this.picOfTheDate = data)

// }
</script>

<style>


#apod {
  text-align: center;
}

</style>