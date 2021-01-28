<template>
    <div>
        <form v-on:submit.prevent="handleDatePic">
            <label for="image_date">Explore the universe by Gregorian date</label>
            <!-- TODO change date picker max value to receive today's date from browser window -->
            <input type="date" id="image_date" name="image_date" min="2015-06-13" max="2021-01-28" v-model="datePic"> 
            <input class='submit' type="submit">
        </form> 
    </div>
</template>

<script>
import { eventBus } from '../main.js';
export default {
    name: 'date-form',
    data() {
        return{
            datePic: null
        }
    },

    methods: {
        handleDatePic() {
            eventBus.$emit('date-picked', this.datePic)
        }
    }
}

</script>

<style>

</style>