<template>
  <div>
    <apod/>

  </div>
</template>

<script>

import Apod from './components/Apod.vue';

export default {
  name: 'app',
  component: {
    'apod' : Apod
  }
}

</script>

<style>

</style>