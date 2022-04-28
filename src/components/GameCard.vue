<template>
  <div class="card game-card">
    <div class="image-wrapper">
      <!-- Image Goes Here -->
      <img :src='image' alt='game image'/>
    </div>
    <div class="info-wrapper flex-col">
      <!-- Game Name Goes Here -->
      <h2>{{ name }}</h2>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'GameCard',
    props: ['name', 'image'],

  }
//   methods: {
//     navigateItem(gameId) {
//       this.$emit('selectGame', gameId)
//     }
//   }
// }
</script>
