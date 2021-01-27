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