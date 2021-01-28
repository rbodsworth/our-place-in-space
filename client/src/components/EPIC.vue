<template>
    <div class="epic-wrapper">
        <h2 class="subtitle">What does our future hold?</h2>
        <h2>EPIC</h2><br>
        <!-- <epic-dates-dropdown class="date-right" :dates="allEpicDates"/> -->
        <img class="epic-image" v-if="archiveImageUrls" :src="archiveImageUrls[0]"/>
        <img class="epic-image" v-else :src="liveEndPoint" />
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
            
            allEpicDatesEndPoint: "https://epic.gsfc.nasa.gov/api/natural/all",
            allEpicDates: [],
            
            selectedDate: null,
            activeDate: null,

            selectedYear: "",
            selectedMonth: "",
            selectedDay: "",
           
            activeYear: "",
            activeMonth: "",
            activeDay: "",

            epicArchiveEndPoint: "",
        
            relevantImageNames: null,
            relevantData: null,
            relevantEndPoint: null,

            imageNames:null,

            imageNamesEndPoint: null,

            archiveEndPointData: [],
            archiveImageNames: [], 
            archiveImageUrls: null,
            
            
            liveEndPoint: "https://api.nasa.gov/EPIC/archive/natural/2019/05/30/jpg/epic_1b_20190530011359.jpg?api_key=II98yPghSJkmCYT5tLCetb1xvGuLEZ4yieHiJDbc",

            mostRecentData: null
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
            console.log(this.selectedYear, 
                        this.selectedMonth, 
                        this.selectedDay)
        },
       
       parseActiveDate: function() {
            let parsed = this.activeDate.split('-');
            this.activeYear = parsed[0]
            this.activeMonth = parsed[1]
            this.activeDay = parsed[2]
        },

        chooseRelevantEndPoint: function(selectedDate) {
            if(selectedDate) {
                this.relevantEndPoint = `https://api.nasa.gov/EPIC/api/natural/date/${this.selectedDate}?api_key=${key.nasa}`
            } else {
                this.relevantEndPoint = `https://api.nasa.gov/EPIC/api/natural/?api_key=${key.nasa}`
            }
            console.log(this.relevantEndPoint)
        },

        mapImageNames: function(data) {
            return data.map (obj => obj.image)
        },

        getTheDate: function() {
                this.activeDate = data[0].date
                console.log(this.activeDate);
        },

        makeImageUrls: function() {
            return this.imageNames.map( image => `https://api.nasa.gov/EPIC/archive/natural/${this.selectedYear}/${this.selectedMonth}/${this.selectedDay}/jpg/${image}.jpg?api_key=${key.nasa}` );
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
       
        .then(this.chooseRelevantEndPoint(this.selectedDate))
        .then(
            fetch(this.relevantEndPoint)
            .then(res => res.json())
            .then(data => this.relevantData = data)),

        eventBus.$on("date-picked", (date) => {
            this.selectedDate = date;
            this.activeDate = date;
            this.parseDate();
            this.parseActiveDate();

            fetch(this.makeEpicArchiveEndPoint())
            .then(res => res.json())
            .then(data => this.archiveEndPointData = data)
            .then(data => this.archiveImageNames = this.mapImageNames(data))
            .then(data => this.archiveImageUrls = this.makeEpicArchiveImageUrls())

            .then(this.chooseRelevantEndPoint(this.selectedDate));

        });
    }

}
</script>

<style>
.epic-wrapper {
    display: flex;
    flex-direction: column;
}

.epic-image {
    mix-blend-mode: screen;
}

</style>