<template>
  <div id='apod'>
    <date-form></date-form>
      <h3> Selected date: {{picOfTheDay.date}}</h3>
      
      <h3> {{picOfTheDay.title}} </h3>
      <div id="caption-picture">
        <img class="apod-image" :src="picOfTheDay.url">
        <section>
        <p class="caption"> {{picOfTheDay.explanation}}</p>
        <p v-if='picOfTheDay.copyright'> Photography Copyright: {{picOfTheDay.copyright}} </p>
        </section>
      </div>

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
    


</script>









<style>
.caption{
  text-align: justify;
  padding: 50px;
  line-height: 2;
  font-size:1vw;
}

#caption-picture {
  display: flex;
  flex-direction: row;
  justify-content: space-around;
  align-items: center;
}

.apod-image {
  width: 50%;
  height: 50%;
  max-width: 1000px;
  max-height: 1000px;
}





</style>