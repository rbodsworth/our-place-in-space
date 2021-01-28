<template>
    <div class="date-picker">
        <!-- <nav>
            <ul>
                <li class="nav-el"><a  class="nav-link" href="#apod">APOD</a></li>
                <li class="nav-el"><a class="nav-link" href="#marsmain">Curiosty</a></li>
                <li class="nav-el"><a class="nav-link" href ="#epic">Epic</a></li>
            </ul>
        </nav> -->
        <form v-on:submit.prevent="handleDatePic">
            <!-- <label for="image_date">Enter a Gregorian date to explore space time</label><br> -->
            <!-- TODO change date picker max value to receive today's date from browser window -->
            <input class="date-input" type="date" id="image_date" name="image_date" min="2015-06-13" max="2021-01-28" v-model="datePic"> 
            <input class='submit submit-button' type="submit" value="Explore">
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


form {
    position: relative;
    width: 100%;
}

.date-picker {
  width: 100%;
  height: 70px;
  margin-left: -15px;
  background-color: #222222;
  position: fixed;
  bottom: 0;
  /* padding: 15px; */
}


.date-input {
    position: absolute;
    left: 15px;
    top: 15px;
    padding: 06px 16px 02px 25px;
    /* bottom: 15px; */
}

.submit-button {
    border-radius: 999px;
    padding: 11px 25px 09px 25px;
    letter-spacing: 1px;
    background-color: #006dff;
    color: #ffffff;
    border-style: none;
    margin-left: auto;
    position: absolute;
    right: 15px;
    top: 15px;
  /* bottom: 15px */
  /* height: 70px */
}

ul{
    display: flex;
    direction: row;
    justify-content: space-between;
    margin: 0 15px;
}


li {
    list-style: none;
}

.nav-link{
    font-family: Arial, Helvetica, sans-serif;
    text-transform: uppercase;
    color: white !important;
    text-decoration: none;
}

</style>