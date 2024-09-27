<template>
  <SearchComponent @search="fetchMovies" />
  <PopularMoviesSection :items="movies" />
</template>

<script>
import SearchComponent from '@/components/SearchComponent.vue'
import PopularMoviesSection from '@/components/PopularMoviesSection.vue'

export default {
name: 'MoviesView',
components: {
  SearchComponent,
  PopularMoviesSection,
},
data() {
  return {
    movies: []
  }
},
methods: {
  async fetchMovies(query = '') {
    try {
      const response = await fetch(`https://api.themoviedb.org/3/search/movie?api_key=348088421ad3fb3a9d6e56bb6a9a8f80&query=${query}`)
      const data = await response.json()
      console.log('API response:', data)
      if (data.results) {
        this.movies = data.results
      } else {
        console.error('No results found.')
      }
    } catch (error) {
      console.error(error)
    }
  }
}
}
</script>
