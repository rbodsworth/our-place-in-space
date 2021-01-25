<template lang="html">
    <div>
        <label for="EPICDates">Choose a date</label>
        <select name="EPICDates">
            <epic-dropdown-item v-for="(item, index) in dates" :date="date"/>
        </select>
    </div>
  
</template>

<script>
import EpicDropdownItem from './EpicDropdownItem';

export default {
    name: 'epicDatesDropdown',

    props: ['dates'],

    components: { "epic-dropdown-item": EpicDropdownItem }
}
</script>

<style>

</style>