<template>
    <button @click='sortGame'> {{ ascending ? 'sort DOWN' : 'sort UP'}} </button>
  <div v-if='games' className="container-grid" >
    <!-- <option :value='parseInt(game.rating)' :key='game.id' >
      rating
    </option> -->
<GameCard :key='game.id' v-for='game in games' :image='game.background_image' :name='game.name' :rating='game.rating' />
  </div>
</template>

<script>
import GameCard from '../components/GameCard.vue'
import axios from 'axios'
  export default {
    name: 'ViewGames',
    data: () => ({
      games: [],
      ascending: true
    }),
    components: {
      GameCard
    },
    mounted() {
      this.getGamesByGenre()
    },
    methods: {
      async getGamesByGenre() {
        const genreId = parseInt(this.$route.params.genre_id)
        const res = await axios.get(`https://api.rawg.io/api/games?genres=${genreId}&key=65f07ae80c4e48d68138324fc56236f8`)
        console.log('5555', genreId)
        this.games = (res.data.results)
        console.log('3333', this.games )
        // Get Genre Id here
      },
      sortGame() {
        if(this.ascending) {
          this.games.sort((a,b) => b.rating - a.rating)
        } else {
        this.games.sort((a,b) => b.rating - a.rating)
        }
        this.ascending = !this.ascending
      }
    }
  }
</script>
