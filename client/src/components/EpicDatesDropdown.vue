<template lang="html">
    <div>
        <label for="EPICDates">Choose a date</label>
        <select name="EPICDates" v-on:change="handleSelect" v-model="selectedDate">
            <epic-dropdown-item v-for="(date, index) in dates" :date="date"/>
        </select>
    </div>
  
</template>

<script>
import EpicDropdownItem from './EpicDropdownItem';
import { eventBus } from '../main';

export default {
    name: 'epicDatesDropdown',
    data() {
        return { "selectedDate": {} }
    },

    props: ['dates'],
    components: { "epic-dropdown-item": EpicDropdownItem },
    methods: {
        handleSelect() {
            eventBus.$emit('date-selected', this.selectedDate)
        }
    }
}
</script>
<style>
</style>