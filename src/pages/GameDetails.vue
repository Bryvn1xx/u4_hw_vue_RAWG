<template>
  <div v-if='gameDetails' class="game-content">
    <section class="image-container">
      <img :src='gameDetails.background_image' alt='details image'/>
      <div>
        <h3>{{ gameDetails.name }} </h3>
        </div>
    </section>
    <section class="details">
      <div class="flex-row space"></div>
      <div>
        <h3></h3>
      </div>
    </section>
  </div>
</template>

<script>
import axios from 'axios'

  export default {
    name: 'GameDetails',
    // props: ['name', 'image'],
    data: () => ({
      gameDetails: null
    }),
    mounted() {
      this.getGameDetails()
    },
    methods: {
      async getGameDetails() {
        const gameId = parseInt(this.$route.params.game_id)
        const res = await axios.get(`https://api.rawg.io/api/games/${gameId}?key=65f07ae80c4e48d68138324fc56236f8`)
        this.gameDetails = (res.data)
        console.log('7778', res.data)

        // this.selectGame()
      }
    }
  }
</script>
