<template>
  <div id='apod'>
      <h2 class="subtitle">When we look to the stars we see ancient history</h2>
      <div class="title-block">
        <h3 v-if="apodData"> {{apodData.title}} </h3>
        <h4 class="date-right" v-if="apodData"> {{apodData.date}}</h4>
      </div>
      <div id="caption-picture">
        <img class="apod-image" v-if="apodData" :src="apodData.url">
        <p v-if='apodData.copyright'> Photography Copyright: {{apodData.copyright}} </p>
        <p v-if="apodData"> {{apodData.explanation}}</p>
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
        datePicked: undefined,
        archiveUrl: undefined,
        apodData: undefined
      }
    },
 
    methods: {
        getApodToday: function(){
            fetch(`https://api.nasa.gov/planetary/apod?api_key=${APIkey}`)
            .then(res => res.json())
            .then(data => this.apodData = data)
        },

        createArchiveUrl: function(date) {
          return this.archiveUrl = `https://api.nasa.gov/planetary/apod?api_key=${APIkey}&date=${this.datePicked}`;
        },
    },

     mounted() {
      this.getApodToday()

      eventBus.$on("date-picked", (date) => {
        this.datePicked = date;
        console.log('offbusdate',this.datePicked);

        fetch(this.createArchiveUrl())
        .then(res => res.json())
        .then(data => this.apodData = data);
      }) 
    },


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

</style>