<template>
  <div>
    <apod></apod>
  </div>
</template>

<script>

import Apod from './components/Apod.vue';

export default {
  name: 'app',
  components: {
    'apod' : Apod
  }
}

</script>

<style>

</style>