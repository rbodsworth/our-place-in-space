<template>

 <div id='apod'>
      <h3> {{photo.name}} </h3>
      <img :src="photo.img_src" width='400' >
      <p id="p1"> Rover name: {{photo.rover.name}} </p>
      <p id="p2"> Sol: {{photo.sol}}</p>
      <p id ="p3"> Earth date: {{photo.earth_date}} </p>
 <!-- <img :src="photo.img_src" width='500' > -->
</div>
</template>

<script>


export default {
    name: "mars-photo-item", 
    props: ['photo']
}
</script>

<style>
#apod {
    display: inline-grid;
    grid-gap: 10px 19px;
    justify-content: space-between;
    padding: 9px;
    margin: -3px;
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
}

#p1,#p2,#p3  {
        margin: -3px;
        padding: 5px;
        font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
       background-color: brown;
       color: cornsilk;

}










</style>