<template>
  <div id="app">
    <div class="container">
      <div class="text-center user-select-none text-light">
        <h2 class="text-center mt-5">{{ today.toLocaleString('en-US', { month: 'long' }) }} {{ today.getYear() + 1900 }} Movies 🍿</h2>
        <p>keep up with popular movie trends</p>
      </div>

      <div class="my-4 user-select-none">
        <a href="#" class="link-warning mx-3 h4 nounderline" @click="getTrendingMovies('day')"> Trending today</a>
        <a href="#" class="link-warning mx-3 h4 nounderline" @click="getTrendingMovies('week')">This week</a>
        <a href="#" class="link-warning mx-3 h4 nounderline" @click="getAdultMovies()">Top Rated All Time</a>
      </div>

      <div class="row" v-if="movies.length > 0">
        <div class="col-md-3" v-for="(movie, i) in movies" :key="i">
          <movie-card :movie="movie" />
        </div>
      </div>

      <!-- TODO: implement pagination -->

    </div>
  </div>
</template>
<style scoped>
  .nounderline {
    text-decoration: none;
  }
</style>
<script>
import MovieCard from "./components/MovieCard.vue";
export default {
  name: "App",
  components: {
    MovieCard,
  },
  data() {
    return {
      movies: [],
      apiKey: process.env.VUE_APP_API_KEY,
      today: new Date()
    };
  },
  methods: {
    getTrendingMovies(category) {
      return fetch(
        `https://api.themoviedb.org/3/trending/movie/${category}?api_key=${this.apiKey}`
      )
        .then((response) => response.json())
        .then((data) => {
          this.movies = data.results;
        })
        .catch(err => console.log('Fetch Error: ', err))
    },
    getAdultMovies() {
      return fetch(
        `https://api.themoviedb.org/3/movie/top_rated?api_key=${this.apiKey}`
      )
        .then((response) => response.json())
        .then((data) => {
          this.movies = data.results;
        })
        .catch(err => console.log('Fetch Error: ', err))
    },
  },
  mounted() {
    this.getTrendingMovies("day");
  },
};
</script>
<style>
  html, body {
    background-color: rgb(37, 37, 37);
  }
</style>