<template>
  <div class="home">
    <div class="feature-card">
      <!-- naruto route -->
      <router-link to="/">
        <img
          class="featured-img"
          src="https://picsum.photos/200/300?random=1"
          alt="Random Poster"
        />
        <div class="description">
          <h3>Random</h3>
          <p>
            Lorem ipsum dolor sit amet consectetur, adipisicing elit.
          </p>
        </div>
      </router-link>
    </div>

    <form @submit.prevent="SearchMovies()" class="search-box">
      <input type="text" placeholder="what are you looking for ?" v-model="search" />
      <input type="submit" value="search" />
    </form>

    <div class="movies-list">
      <div class="movie" v-for="movie in movies" :key="movie.imdbID">
        <router-link :to="'/movie/' + movie.imdbID" class="movie-link">
          <div class="product-image">
            <img :src="movie.Poster" alt="Movie Poster" />
            <div class="type">{{ movie.Type }}</div>
          </div>
          <div class="detail">
            <p class="y">{{ movie.Year }}</p>
            <h3>{{ movie.Title }}</h3>
          </div>
        </router-link>
      </div>
    </div>
  </div>
</template>

<script>
  import { ref } from "vue"
  import env from "@/env"
  export default {
    name: "Home",
    setup() {
      const search = ref("")
      const movies = ref([])
      const SearchMovies = () => {
        if (search.value != "") {
          // console.log(search.value)
          fetch(`http://www.omdbapi.com/?apikey=${env.apikey}&s=${search.value}`)
            .then((response) => response.json())
            .then((data) => {
              movies.value = data.Search
              search.value = ""
              // console.log(movies.value)
            })
        }
      }

      return {
        search,
        movies,
        SearchMovies,
      }
    },
  }
</script>

<style lang="scss">
  .home {
    .feature-card {
      position: relative;
    }
    .featured-img {
      display: block;
      width: 100%;
      height: 300px;
      object-fit: cover;
      position: relative;
      z-index: 0;
    }
    .description {
      position: absolute;
      left: 0;
      right: 0;
      bottom: 0;
      background: linear-gradient(to bottom, rgba(0, 0, 0, 0), rgba(0, 0, 0, 0.8));
      padding: 16px;
      z-index: 1;
      h3 {
        color: #fff;
        margin-bottom: 16px;
      }
      p {
        color: white;
      }
    }
    .search-box {
      display: flex;
      flex-direction: column;
      justify-content: center;
      padding: 16px;
      align-items: center;

      input {
        display: block;
        appearance: none;
        border: none;
        outline: none;
        background: none;

        &[type="text"] {
          width: 100%;
          padding: 10px 16px;
          margin-bottom: 15px;
          transition: 0.4s;
          display: block;
          font-size: 1rem;
          font-weight: 400;
          line-height: 1.5;
          color: #28a745;
          background-color: #fff;
          background-clip: padding-box;
          border: 1px solid #ced4da;
          border-radius: 0.25rem;
          transition: border-color 0.15s ease-in-out, box-shadow 0.15s ease-in-out;

          &::placeholder {
            color: #17a2b8;
          }
          &:focus {
            box-shadow: 0px 3px 6px rgba(0, 0, 0, 0.2);
          }
        }
        &[type="submit"] {
          width: 100%;
          max-width: 300px;
          background: #007bff;
          padding: 16px;
          border-radius: 8px;
          color: #fff;
          font-style: 20px;
          text-transform: uppercase;
          transition: 0.4s;

          &:active {
            background-color: #0062cc;
            box-shadow: 0 0 0 0.2rem rgba(38, 143, 255, 0.5);
          }
        }
      }
    }
    .movies-list {
      display: flex;
      flex-direction: column;
      flex-wrap: wrap;
      margin: 0px 8px;

      .movie {
        max-width: 100%;
        flex: 1 1 100%;
        padding: 16px 8px;

        .movie-link {
          display: flex;
          flex-direction: column;
          height: 100%;

          .product-image {
            position: relative;
            display: block;

            img {
              display: block;
              width: 100%;
              height: 275px;
              object-fit: cover;
            }

            .type {
              position: absolute;
              padding: 8px 16px;
              background-color: #42b883;
              color: #fff;
              bottom: 16px;
              left: 0;
              text-transform: capitalize;
            }
          }
          .detail {
            background: #2b90d9;
            padding: 16px 8px;
            flex: 1 1 100%;
            border-radius: 0 0 8px 8px;
            p {
              color: #fff;
            }
            h3 {
              color: #fff;
            }
          }
        }
      }
    }
  }
</style>
