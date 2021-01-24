<template>
    <div>
        <form v-on:submit.prevent="handleDateSubmit">
            <label for="image_date">Select a date</label>
            <input type="date" id="image_date" name="image_date" v-model="date_selected">
            <input type="submit">
        </form> 
        
        <!-- <h3 v-if="picOfTheDate"> {{picOfTheDate.title}} </h3>
        <h3 v-if="picOfTheDate"> {{picOfTheDate.explanation}} </h3>
        <h3 v-if="picOfTheDate"> {{picOfTheDate.date}} </h3>
        <img v-if="picOfTheDate" :src="picOfTheDate.url" width='500'> -->
    </div>
  
</template>

<script>
import { APIkey } from '../assets/APOD-API-Key';
import { eventBus } from '../main.js';
export default {
    name: 'date-form',
    data() {
        return{
            date_selected: undefined,
            picOfTheDate: undefined

        }
    },
    methods: {
        handleDateSubmit: function(){
            // fetch(`https://api.nasa.gov/planetary/apod?api_key=${APIkey}`)
            fetch (`https://api.nasa.gov/planetary/apod?api_key=${APIkey}&date=${this.date_selected}`)
            .then ( res => res.json())
            .then (data => this.picOfTheDate = data)

            eventBus.$emit("selected-date", this.picOfTheDate)
        }
    }
}
</script>

<style>

</style>