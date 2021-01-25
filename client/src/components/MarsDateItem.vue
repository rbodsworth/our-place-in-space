<template>
    <div>
        <form v-on:submit.prevent="handleDateSubmit">
            <label for="image_date">Select a date</label>
            <input type="date" id="image_date" name="image_date" v-model="date_selected">
            <input type="submit">
        </form> 
</template>

<script>

import { APIkey } from '@/assets/MARS_API_KEY'

export default {
    name: 'mars-date-item',
    data () {
        return {
            selectedDate: null 

        }
    },

    methods: {
      getPhotos: function(){
      fetch(`https://api.nasa.gov/mars-photos/api/v1/rovers/curiosity/photos?earth_date=${date}&api_key=${APIkey}`)
      .then( res => res.json())
      .then(data => this.selectedDate = data)

}}}


</script>

<style>

</style>