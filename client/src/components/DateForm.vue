<template>
    <div>
        <form v-on:submit.prevent="handleDatePic">
            <label for="image_date">Search images by a specific date</label>
            <input class="date" type="date" id="image_date" name="image_date" v-model="datePic">
            <input class='submit' type="submit">
        </form> 
    </div>
  
</template>

<script>
import { APIkey } from '../assets/APOD-API-Key';
import { eventBus } from '../main.js';
export default {
    name: 'date-form',
    data() {
        return{
            datePic: null
            // picOfTheDate: null
        }
    },

    methods: {
        handleDatePic() {
            eventBus.$emit('date-picked', this.datePic)
            console.log('datePicked', datePic);
            // console.log('date_selected_form', date_selected_form);
        }
    }
}

        // handleDateSubmit(){
        //     fetch (`https://api.nasa.gov/planetary/apod?api_key=${APIkey}&date=${this.date_selected_form}`)
        //     .then ( res => res.json())
        //     .then ((picOfTheDate) => {
        //         this.picOfTheDate = picOfTheDate
        //         eventBus.$emit("date-selected", this.picOfTheDate)
        //         eventBus.$emit("date-test", this.picOfTheDate.date)
        //     })


</script>

<style>

</style>