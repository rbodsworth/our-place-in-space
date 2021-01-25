<template>
    <div>
        <form v-on:submit.prevent="handleDateSubmit">
            <label for="image_date">Select a date</label>
            <input type="date" id="image_date" name="image_date" v-model="selected_date">
            <input type="submit">
        </form> 

            </div>
</template>

<script>

import { APIkey } from '@/assets/MARS_API_KEY'
import { eventBus } from '../main.js';

export default {
    name: 'mars-date-item',
    data () {
        return {
            selected_date: undefined,
            datePic: undefined

        }
    },

    methods: {
      handleDateSubmit: function(){
      fetch(`https://api.nasa.gov/mars-photos/api/v1/rovers/curiosity/photos?earth_date=${this.selected_date}&api_key=${APIkey}`)
      .then( res => res.json())
      .then(data => this.datePic = data)

    eventBus.$emit("selected-date", this.datePic)


}}}


</script>

<style>

</style>