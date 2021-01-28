<template>
    <div>
        <form v-on:submit.prevent="handleDatePic">
            <label for="image_date">Explore the universe by Gregorian date</label>
            <!-- TODO change date picker max value to receive today's date from browser window -->
            <input type="date" id="image_date" name="image_date" min="2015-06-13" max="2021-01-28" v-model="datePic"> 
            <input class='submit submit-button' type="submit">
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


/**
 * 1. Change the font styles in all browsers.
 * 2. Remove the margin in Firefox and Safari.
 */

button,
input,
optgroup,
select,
textarea {
  font-family: Helvetica, Arial, sans-serif; /* 1 */
  font-size: 100%; /* 1 */
  line-height: 1.15; /* 1 */
  margin: 0; /* 2 */
}

/**
 * Show the overflow in IE.
 * 1. Show the overflow in Edge.
 */

button,
input { /* 1 */
  overflow: visible;
}

/**
 * Remove the inheritance of text transform in Edge, Firefox, and IE.
 * 1. Remove the inheritance of text transform in Firefox.
 */

button,
select,
input { /* 1 */
  text-transform: uppercase;
  
}

/**
 * Correct the inability to style clickable types in iOS and Safari.
 */

button,
[type="button"],
[type="reset"],
[type="submit"] {
  -webkit-appearance: button;
}


.submit-button {
    border-radius: 999px;
  padding: 09px 25px 08px 25px;
  letter-spacing: 1px;
  background-color: #006dff;
  color: #ffffff;
  border-style: none;
}




</style>