<template>
  <div>
    <h2>{{movie.Title}}</h2>
    <p>{{movie.Year}}</p>
    <img :src="movie.Poster" alt="Movie Poster" />
    <p>{{movie.Plot}}</p>
  </div>
</template>

<script>
import { useRoute } from 'vue-router'
import { ref, onBeforeMount } from 'vue'
export default {
  setup() {
    const movie = ref({})
    const route = useRoute()

    onBeforeMount(() => {
      fetch(`http://www.omdbapi.com/?apikey=6a26ba6&i=${route.params.id}&plot=full`)
        .then(response => response.json())
        .then(data => {
          movie.value = data 
        })
    })

    return { movie }
  }
}
</script>

<style scoped>
h2 {
  color: #fff;
  text-transform: uppercase;
}

p {
  color: #fff;
}

p:nth-last-of-type(1) {
  line-height: 32px;
}
</style>