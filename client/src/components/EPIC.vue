<template>
    <div>
        <h2>EPIC</h2><br>
        <span>with this {{this.epicImage}}</span><br>
        <span>without {{epicImage}}</span>
    </div>
</template>

<script>
export default {
    name: 'epic-image',
    data() {
        return {
            epicImage: undefined,
            url: "https://epic.gsfc.nasa.gov/archive/natural/2015/10/31/png/epic_1b_20151031074844.png"
        }
    },
    methods: {
        getEpicImage: function() {
            fetch(this.url)
            .then(res => this.epicImage = res)
        }
    },
    mounted() {
        this.getEpicImage()
    }

}
</script>

<style>

</style>