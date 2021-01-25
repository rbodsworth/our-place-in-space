<template>
    <div>
        <h2>EPIC</h2><br>
        <span>with this {{this.epicImage}}</span><br>
        <span>without {{epicImage}}</span>
        <epic-dates-dropdown :dates="allEpicDates"/>
        <button v-on:click="getEpicArchivebyDate()">Archive</button>
        <button v-on:click="getEpicRecent()">Today</button>
        <button v-on:click="makeEpicArchiveEndPoint()">Make end point</button>
        <img :src="liveEndPoint"/>
    </div>
</template>

<script>
import key from '../secrets/rAPI.json';
import EpicDatesDropdown from './EpicDatesDropdown';
import { eventBus } from '../main.js';


export default {
    name: 'epic-image',
    components : {
        "epic-dates-dropdown": EpicDatesDropdown
    },
    data() {
        return {
            epicImage: null,
            testUrl: "https://api.nasa.gov/EPIC/archive/natural/2019/05/30/jpg/epic_1b_20190530011359.jpg?api_key=",
            
            allEpicDatesEndPoint: "https://epic.gsfc.nasa.gov/api/natural/all",
            allEpicDates: [],
            selectedDate: "",

            selectedYear: "",
            selectedMonth: "",
            selectedDay: "",

            
            epicMostRecentEndPoint: "https://api.nasa.gov/EPIC/api/natural/?api_key=",
            epicArchiveEndPoint: "",
            
            
            liveEndPoint: "",
            inputDate:""
        }
    },
    methods: {
        // addApiKeyToUrl: function () {
        //     return this.liveEndPoint =  this.testUrl + key.nasa;
        // },

        addApiKeyToEndPoint: function(endPoint) {
            return this.liveEndPoint =  endPoint + key.nasa;
        },

        getEpicImage: function() {
            this.addApiKeyToUrl()
            fetch(this.liveEndPoint)
            // .then(console.log(res))
            .then(res => this.epicImage = res)
            .then(console.log(this.epicImage));
        },

        getEpicRecent: function() {
            this.addApiKeyToEndPoint(this.epicMostRecentEndPoint);
            console.log(this.liveEndPoint);
        },

        parseDate: function() {
            let parsed = this.selectedDate.split('-');
            this.selectedYear = parsed[0]
            this.selectedMonth = parsed[1]
            this.selectedDay = parsed[2]
            console.log(this.selectedYear, this.selectedMonth, this.selectedDay)
        },

        makeEpicArchiveEndPoint: function() {
            return this.epicArchiveEndPoint  = `https://api.nasa.gov/EPIC/archive/natural/${this.selectedYear}/${this.selectedMonth}/${this.selectedDay}/?api_key=${key.nasa}`;
        }




            // inputDate = '2018-08-12'
            // fetch(this.liveEndPoint)
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

        eventBus.$on("date-selected", (selectedDate) => {
            this.selectedDate = selectedDate;
            console.log(this.selectedDate);
            this.parseDate();
        });
    }

}
</script>

<style>

</style>