<template>
    <div>
        <p>This is where the date form will appear</p>
        <!-- on submission of form, call function handleDateSubmit()
        which should make a new Api call with the date value as a parameter.
        This should result in an image that corresonds to that date -->
    </div>
  
</template>

<script>
export default {
    name: 'date-form',
    data() {
        return{
            date_selected: undefined
        }
    },
    methods: {
        handleDateSubmit: function(){
            // get date inputted/selected by user in form 
            // update this.date_selected?
          // fetch data from api using selected date as a parameter
          // new request should return a json response that includes new image and assoc details

        }
    }

}
</script>

<style>

</style>