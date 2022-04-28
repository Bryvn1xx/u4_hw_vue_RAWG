<template>
  <div>
    <div class="search">
      <!-- Search Form Goes Here -->
      <h2>Search Results</h2>
      <section class="search-results container-grid">
        <GameCard @click='selectGame(game.id)' :name='game.name' :image='game.background_image' :key='game.id' v-for='game in searchResults'/>
        <!-- <GameDetails :name='game.name'/> -->
        
          <form @submit='getSearchResults'>
            <input
            @input='handleChange'
            type='search'
            name='search'
            :value='searchQuery'
            placeholder='search games'
            >
            <button className='button' text='submit'></button>
            
          </form>
        
      </section>
    </div>

    <div class="genres" v-if='!searched'>
      <h2>Genres</h2>
      <section class="container-grid">
        <GenreCard :genres='genres' :image='genre.image_background' :name='genre.name' :key='genre.id' v-for='genre in genres'/>
      </section>
    </div>
  </div>
</template>

<script>
  import axios from 'axios'
  import GenreCard from '../components/GenreCard.vue'
  import GameCard from '../components/GameCard.vue'
  // import GameDetails from '../components/GameDetails'
  // const API_KEY = process.env.RAWG_API_KEY
  export default {
    name: 'HomePage',
    components: {
      GenreCard,
      GameCard
    },
    data: () => ({
      genres: [],
      searchQuery: '',
      searchResults: [],
      searched: false
    }),
    mounted() {
      this.getGenres()      
    },
    methods: {
      async getGenres() {
        const res = await axios.get(`https://api.rawg.io/api/genres?key=65f07ae80c4e48d68138324fc56236f8`)
        this.genres = res.data.results
        console.log(this.genres)
      },
      async getSearchResults(e) {
        e.preventDefault()
        const res = await axios.get(`https://api.rawg.io/api/games?key=65f07ae80c4e48d68138324fc56236f8&search=${this.searchQuery}`)
        this.searchResults = (res.data.results)
        // console.log('0987654', res.data)
        // this.searchResults('')
        console.log('srrr', this.searchResults)

      },
      handleChange(event) {
        this.searchQuery = event.target.value
        this.searched = !this.searched

        console.log('3456789', this.genre)
      },
      selectGame(gameId) {
        this.$router.push(`/details/${gameId}`)
        console.log('gameId', gameId)
        // this.selectGame()
      }
    }
  }
</script>
