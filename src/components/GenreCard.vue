<template>
  <div class="card">
    <div class="image-wrapper">
      <!-- Image Goes Here -->
      <img :src='image' alt='genre image' /> 

    </div>
    <div class="info-wrapper flex-col">
      <!-- Genre Name Goes Here -->
      <h2>{{ name }} </h2>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'GenreCard',
    props: ['name', 'image' ]
  }
  
</script>
