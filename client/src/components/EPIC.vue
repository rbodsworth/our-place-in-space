<template>
    <div>
        <h2>EPIC</h2><br>
        <span> 01</span>
        <epic-dates-dropdown :dates="allEpicDates"/>
        <img v-if="archiveImageUrls" :src="archiveImageUrls[0]"/>
        <img v-else :src="liveEndPoint" />
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
            selectedDate: null,

            selectedYear: "",
            selectedMonth: "",
            selectedDay: "",

            epicArchiveEndPoint: "",
            
            epicMostRecentEndPoint: "https://api.nasa.gov/EPIC/api/natural/?api_key=", //returns obj with image names
            mostRecent: null,

            imageNamesEndPoint: null,

            archiveEndPointData: [],
            archiveImageNames: [], 
            archiveImageUrls: null,
            
            
            liveEndPoint: "https://api.nasa.gov/EPIC/archive/natural/2019/05/30/jpg/epic_1b_20190530011359.jpg?api_key=II98yPghSJkmCYT5tLCetb1xvGuLEZ4yieHiJDbc",
            // mostRecentEndPoint: "https://api.nasa.gov/EPIC/archive/natural", //returns nada

            mostRecentData: null
            // add api key, get image name, get url
        }
    },
    methods: {

        addApiKeyToEndPoint: function(endPoint) {
            return this.liveEndPoint =  endPoint + key.nasa;
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

        makeRelevantEndPoint: function(selectedDate) {
            if(selectedDate) {
                this.imageNamesEndPoint = `https://api.nasa.gov/EPIC/api/natural/date/${this.selectedDate}?api_key=${key.nasa}`;
            } else {
                this.imageNamesEndPoint = `https://api.nasa.gov/EPIC/api/natural/?api_key=${key.nasa}`
            }
            console.log(this.imageNamesEndPoint);
        },

        makeEpicMostRecentEndPoint: function() {
            this.mostRecent = `https://api.nasa.gov/EPIC/api/natural/?api_key=${key.nasa}`
        },

        makeEpicArchiveEndPoint: function() {
            return this.epicArchiveEndPoint  = `https://api.nasa.gov/EPIC/api/natural/date/${this.selectedDate}?api_key=${key.nasa}`;
        },

        getArchiveImageNames: function(data) {
            return data.map( obj => obj.image );
        },

        makeEpicArchiveImageUrls: function() {
            return this.archiveImageNames.map( image => `https://api.nasa.gov/EPIC/archive/natural/${this.selectedYear}/${this.selectedMonth}/${this.selectedDay}/jpg/${image}.jpg?api_key=${key.nasa}` );
        }
    },

    mounted() {
        fetch(this.allEpicDatesEndPoint)
        .then(res => res.json())
        .then(data => this.allEpicDates = data)
       
       .then(this.makeRelevantEndPoint(this.selectedDate))

        // .then(fetch(this.mostRecentEndPoint))
        // .then(res => res.json())
        // .then(data => mostRecentData = data)
        // .then(console.log(mostRecentData));


        eventBus.$on("date-selected", (selectedDate) => {
            this.selectedDate = selectedDate;
            console.log(this.selectedDate);
            this.parseDate();

            fetch(this.makeEpicArchiveEndPoint())
            .then(res => res.json())
            .then(data => this.archiveEndPointData = data)
            .then(data => this.archiveImageNames = this.getArchiveImageNames(data))
            .then(data => this.archiveImageUrls = this.makeEpicArchiveImageUrls())

            .then(this.makeRelevantEndPoint(this.selectedDate));
        });
    }

}
</script>

<style>

</style>