<template>
  <div class="title">
    <h1>Find any Movie</h1>
  </div>
  <form @submit.prevent="SearchMovies()">
    <input type="text" placeholder="type name of the movie" v-model="search" class="input" />
    <input type="submit" value="Search" class="submitInput" />
  </form>
  <div v-for="movie in movies" :key="movie.imdbID" class="movie-list">
    <div class="movie">
      <router-link :to="'/movie/' + movie.imdbID">
      <img :src="movie.Poster" alt="Movie Poster">
      <div class="typeMovie">{{movie.Type}}</div>
    </router-link>
    </div>
  </div>
</template>

<script>
import { ref } from 'vue'
export default {
  setup() {
    const search = ref('')
    const movies = ref([])

    const SearchMovies = () => {
      if (search.value != '') {
        fetch(`http://www.omdbapi.com/?apikey=6a26ba6&s=${search.value}`)
          .then(response => response.json()) 
          .then(data => {
            movies.value = data.Search
            search.value = ''
          })
      }
    }

    return { search, movies, SearchMovies }
  }
}
</script>

<style scoped>
.input {
  border-radius: 5px;
  width: 290px;
  border: 2px solid #eaeaea;
  padding: 20px;
  outline: none;
  margin: 3px;
  margin-bottom: 30px;
}

.submitInput {
    height: 50px;
    width: 80px;
    border-radius: 5px;
    border: 1px solid #87cb84;
    background-color: #87cb84;
    padding: 8px 15px;
    outline: none;
    font-size: 14px;
    font-weight: 700;
    color: #fff;
    cursor: pointer;
    transition: all 0.3s ease;
    margin: 3px;
  }
  .submitInput:hover{
    background-color: #70a66f;
  }

  h1 {
    color: #ffffff;
  }

  .title {
    background-color: #DB5205;
  }

  .movie-list {
    padding-left: 0;
    display: inline-block;
  }

  .movie {
    margin: 3px;
    background-color: #E1CFCF;
  }

  img {
    width: 300px;
    height: 400px;
  }

  .typeMovie {
    background-color: #283D72;
    color: #E1CFCF;
    text-transform: uppercase;
    font-weight: 700;
  }
</style>