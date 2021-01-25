<template>
    <div>
        <h2>EPIC</h2><br>
        <span>with this {{this.epicImage}}</span><br>
        <span>without {{epicImage}}</span>
        <button v-on:click="getEpicArchivebyDate()">Archive</button>
        <button v-on:click="getEpicRecent()">Today</button>
        <img :src="workingUrl"/>
    </div>
</template>

<script>
import key from '../secrets/rAPI.json';


export default {
    name: 'epic-image',
    data() {
        return {
            epicImage: undefined,
            testUrl: "https://api.nasa.gov/EPIC/archive/natural/2019/05/30/jpg/epic_1b_20190530011359.jpg?api_key=",
            // epicArchiveEndPoint: `https://api.nasa.gov/EPIC/archive/natural/?api_key=`,
            allEpicDatesEndPoint: "https://epic.gsfc.nasa.gov/api/natural/all",
            allEpicDates: {},
            epicMostRecentEndPoint: "https://api.nasa.gov/EPIC/api/natural/?api_key=",
            workingUrl: "",
            inputDate:""
        }
    },
    methods: {
        // addApiKeyToUrl: function () {
        //     return this.workingUrl =  this.testUrl + key.nasa;
        // },

        addApiKeyToEndPoint: function(endPoint) {
            return this.workingUrl =  endPoint + key.nasa;
        },

        getEpicImage: function() {
            this.addApiKeyToUrl()
            fetch(this.workingUrl)
            // .then(console.log(res))
            .then(res => this.epicImage = res)
            .then(console.log(this.epicImage));
        },

        getEpicRecent: function() {
            this.addApiKeyToEndPoint(this.epicMostRecentEndPoint);
            console.log(this.workingUrl);
        },

        // getEpicArchivebyDate: function() {
        //     this.addApiKeyToEndPoint(this.epicArchiveEndPoint);
        //     console.log(this.workingUrl);

            // inputDate = '2018-08-12'
            // fetch(this.workingUrl)
        // },

        // query json 
        // findFirstIndexFromPartVal: (arr, key, query) => { 
            // return arr.findIndex(el => el[(key)].indexOf(query) !== -1 )
            // }
    },
    mounted() {
        // this.getEpicImage()
        fetch(this.allEpicDatesEndPoint)
        .then(res => res.json())
        .then(data => this.allEpicDates = data)
    }

}
</script>

<style>

</style>