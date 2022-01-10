<template>
  <div class="home">
    <Hero />
    <Movies :movies="movies"/>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'IndexPage',
  data: () => ({
    movies: [],
  }),
  async fetch() {
    await this.fetchMovies()
  },
  methods: {
    async fetchMovies() {
      const movieApiKey = process.env.movieApiKey
      const data = axios.get(
        `https://api.themoviedb.org/3/movie/now_playing?api_key=${movieApiKey}&language=en-US&page=1`
      )
      const result = await data
      this.movies = result.data.results

      // result.data.results.forEach((movie) => {
      //   this.movies.push(movie)
      // })
    },
  },
}
</script>
