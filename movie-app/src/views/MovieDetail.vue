<template>
  <div class="movie-detail">
    <h2>{{ movie.Title }}</h2>
    <p>Year : {{ movie.Year }}</p>
    <img :src="movie.Poster" alt="Movie Poster" class="feature-img" />
    <p>{{ movie.Plot }}</p>
  </div>
</template>

<script>
  import { ref, onBeforeMount } from "vue"
  import { useRoute } from "vue-router"
  import env from "@/env"
  export default {
    setup() {
      const movie = ref({})
      const route = useRoute()
      onBeforeMount(() => {
        fetch(`http://www.omdbapi.com/?apikey=${env.apikey}&i=${route.params.id}&plot=full`)
          .then((response) => response.json())
          .then((data) => {
            movie.value = data
            console.log(env)
          })
      })
      return {
        movie,
        route,
      }
    },
  }
</script>

<style lang="scss" scoped>
  .movie-detail {
    padding: 10px;
    text-align: center;
    h2 {
      color: #f35022;
      font-size: 28px;
      font-weight: 400;
      margin-bottom: 10px;
    }

    .feature-img {
      display: block;
      width: 100%;
      margin: 5px 0 15px 0;
    }
    p {
      color: #000;
      font-size: 18px;
      line-height: 1.4;
    }
  }
</style>
