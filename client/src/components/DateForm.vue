<template>
    <div>
        <p>This is where the date form will appear</p>
        <form v-on:submit.prevent="handleDateSubmit">
            <label for="image_date">Select a date</label>
            <input type="date" id="image_date" name="image_date" v-model="date_selected">
            <input type="submit">
        </form> 
        <!-- on submission of form, call function handleDateSubmit()
        which should make a new Api call with the date value as a parameter.
        This should result in an image that corresonds to that date -->
        <h3 v-if="picOfTheDate"> {{picOfTheDate.title}} </h3>
        <h3 v-if="picOfTheDate"> {{picOfTheDate.explanation}} </h3>
        <h3 v-if="picOfTheDate"> {{picOfTheDate.date}} </h3>
        <img v-if="picOfTheDate" :src="picOfTheDate.url" width='500'>
    </div>
  
</template>

<script>
import { APIkey } from '../assets/APOD-API-Key';
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


        // the date collected needs to trigger a new date-specific fetch
        // data from date speific fetch to be put in "variable"


            // update this.date_selected?
          // fetch data from api using selected date as a parameter
          // new request should return a json response that includes new image and assoc details

        }
    }
}
</script>

<style>

</style>