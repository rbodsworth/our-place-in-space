<template>
    <div>
        <h2>EPIC</h2><br>
        <span> 01</span>
        <epic-dates-dropdown :dates="allEpicDates"/>
        <button v-on:click="getArchiveImageNames()">02 GetImageNames</button>
        <button v-on:click=" makeEpicArchiveImageUrls()">03 Make Urls</button>
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
            // testUrl: "https://api.nasa.gov/EPIC/archive/natural/2019/05/30/jpg/epic_1b_20190530011359.jpg?api_key=",
            
            allEpicDatesEndPoint: "https://epic.gsfc.nasa.gov/api/natural/all",
            allEpicDates: [],
            selectedDate: "",

            selectedYear: "",
            selectedMonth: "",
            selectedDay: "",

            epicArchiveEndPoint: "",
            
            epicMostRecentEndPoint: "https://api.nasa.gov/EPIC/api/natural/?api_key=",
            archiveEndPointData: [],
            archiveImageNames: [], 
            archiveImageUrls: [],
            
            
            liveEndPoint: "",
        }
    },
    methods: {

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
            return this.epicArchiveEndPoint  = `https://epic.gsfc.nasa.gov/api/natural/date/${this.selectedDate}?api_key=${key.nasa}`;
        },

        getArchiveImageNames: function() {
            this.archiveEndPointData.forEach( el => console.log('image name', el.image) );
            this.archiveEndPointData.forEach( el => this.archiveImageNames.push(el.image) );
        },

        makeEpicArchiveImageUrls: function() {
            return this.archiveImageUrls = this.archiveImageNames.map( image => `https://api.nasa.gov/EPIC/archive/natural/${this.selectedYear}/${this.selectedMonth}/${this.selectedDay}/jpg/${image}.jpg?api_key=${key.nasa}` )
        }

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

            fetch(this.makeEpicArchiveEndPoint())
            .then(res => res.json())
            .then(data => this.archiveEndPointData = data);
            // .then(this.getArchiveImageNames());
            // .then(this.makeEpicArchiveImageUrls());

        });
    }

}
</script>

<style>

</style>