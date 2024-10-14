<template>
  <div>
    <SearchComponent @search="fetchMovies" />
    <PopularMoviesSection :items="movies" />
  </div>
</template>

<script>
import SearchComponent from '@/components/SearchComponent.vue'
import PopularMoviesSection from '@/components/PopularMoviesSection.vue'

export default {
  name: 'MoviesView',
  components: {
    SearchComponent,
    PopularMoviesSection
  },
  data() {
    return {
      movies: []
    }
  },
  mounted() {
    this.fetchMovies();
  },
  methods: {
    async fetchMovies(query = '') {
      try {
        const url = query
          ? `https://api.themoviedb.org/3/search/movie?api_key=348088421ad3fb3a9d6e56bb6a9a8f80&query=${ encodeURIComponent(query) }`
          : `https://api.themoviedb.org/3/movie/popular?api_key=348088421ad3fb3a9d6e56bb6a9a8f80`;
        const response = await fetch(url);
        const data = await response.json();

        if (data.results) {
          console.log(data.results)
          this.movies = data.results;
        } else {
          console.error('No results found.');
        }
      } catch (error) {
        console.error('Error fetching movies:', error);
      }
    }
  }
}
</script>