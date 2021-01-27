<template lang="html">
    <div>
        <label for="EPICDates">Choose a date</label>
        <select name="EPICDates" v-on:change="handleSelect" v-model="selectedDate">
            <option value="date" v-for="(date, index) in dates" :value="date.date">{{ date.date }}</option>
        </select>
    </div>
  
</template>

<script>
import { eventBus } from '../main';

export default {
    name: 'epicDatesDropdown',
    data() {
        return { "selectedDate": {} }
    },

    props: ['dates'],
    methods: {
        handleSelect() {
            eventBus.$emit('epic-date-selected', this.selectedDate)
        }
    }
}
</script>
<style>
</style>