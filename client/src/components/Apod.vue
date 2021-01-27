<template>
  <div id='apod'>
      <h2 class="subtitle">When we look to the stars we see ancient history</h2>
      <div class="title-block">
        <h3 v-if="picOfTheDay"> {{picOfTheDay.title}} </h3>
        <h4 class="date-right" v-if="picOfTheDay"> {{picOfTheDay.date}}</h4>
      </div>
      <div id="caption-picture">
        <img class="apod-image" v-if="picOfTheDay" :src="picOfTheDay.url">
        <p v-if='picOfTheDay.copyright'> Photography Copyright: {{picOfTheDay.copyright}} </p>
        <p v-if="picOfTheDay"> {{picOfTheDay.explanation}}</p>
      </div>
    <!-- <date-form class="date-input"></date-form> -->
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
        // picOfTheDay: undefined
        datePicked: undefined
      }
    },

    mounted () {
      this.getApodToday()
      // eventBus.$on("date-picked", (payload) => this.picOfTheDay = payload)
      eventBus.$on("date-picked", (date => this.datePicked = date))
    },
    
    methods: {
        getApodToday: function(){
            fetch(`https://api.nasa.gov/planetary/apod?api_key=${APIkey}`)
            .then(res => res.json())
            .then(data => this.picOfTheDay = data)
        },

        getApodByDate: function(){

        }
        }
}
    


</script>




<style>

#apod {
  display: flex;
  flex-direction: column;
}

.subtitle {
  font-family: Georgia, 'Times New Roman', Times, serif;
  font-weight: 100;
  font-style: italic;
  text-transform: initial;
}

/* #caption-picture {
  display: flex;
  flex-direction: column;
  justify-content: space-around;
  align-items: center;
} */



/* .apod-image { */
  /* width: 50%; */
  /* height: 50%; */
  /* max-width: 1000px; */
  /* max-height: 1000px; */
/* } */

</style>