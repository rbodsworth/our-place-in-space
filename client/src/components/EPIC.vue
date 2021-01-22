<template>
    <div>
        <h2>EPIC</h2><br>
        <span>with this {{this.epicImage}}</span><br>
        <span>without {{epicImage}}</span>
    </div>
</template>

<script>
import key from '../secrets/rAPI.json';

export default {
    name: 'epic-image',
    data() {
        return {
            epicImage: undefined,
            url: "https://api.nasa.gov/EPIC/archive/natural/2019/05/30/jpg/epic_1b_20190530011359.jpg?api_key=",
            workingUrl: ""
        }
    },
    methods: {
        generateFullUrl: function () {
            return this.workingUrl =  this.url + key.nasa;
        },

        getEpicImage: function() {
            this.generateFullUrl()
            fetch(this.workingUrl)
            // .then(console.log(res))
            .then(res => this.epicImage = res)
            .then(console.log(this.epicImage));
        }
    },
    mounted() {
        this.getEpicImage()
    }

}
</script>

<style>

</style>