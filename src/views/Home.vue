<template>
  <div class="home">
    <main id="main" class="index">
      <section class="inner_content new_index">
        <div id="media_v4" class="media discover">
          <div class="column_wrapper">
          <div class="content_wrapper wrap">
            <div class="title">
              <h2>Welcome</h2>
              <h3>Millions of movies to discover. Explore now.</h3>
            </div>
            <div class="search">
            <form @submit.prevent="SearchMovies()" class="search-box" id="inner_search_from">
             <label>
               <input dir="auto" id="inner_search_v4" name="query" type="text" tabindex="1" autocorrect="off" autofill="off" autocomplete="off" spellcheck="false" placeholder="Search for a movie......"  v-model="search">
             </label>
              <input type="submit" value="Search">
            </form>
            </div>
          </div>
          </div>
        </div>
      </section>
    </main>
    <div class="movies-list">
      <div class="movie" v-for="movie in movies" :key="movie.id">
        <router-link :to="'/movie/' + movie.id" class="movie-link">
          <div class="product-image">
            <img :src="'https://image.tmdb.org/t/p/w500'+movie.backdrop_path" alt="Movie Poster" />
          </div>
          <div class="detail">
            <p class="year">Release Date : {{ movie.release_date }}</p><br>
            <h3>{{ movie.title }}</h3>
          </div>
        </router-link>
      </div>
    </div>
  </div>

</template>

<script>
import { ref } from 'vue';
import env from '@/env.js'

export default {

  setup () {
    const search = ref("");
    const movies = ref([]);
    const SearchMovies = () => {

      if (search.value != "") {
        //console.log('test');
        fetch(`https://api.themoviedb.org/3/search/movie?api_key=${env.apikey}&query=${search.value}`)
            .then(response => response.json())
            .then(data => {
               console.log(data.results);
               movies.value = data.results;
               search.value = "";
            });
      }
    }
    return {
      search,
      movies,
      SearchMovies,
      // Navbar
    }
  }
}
</script>

<style lang="scss">
.home {

  .feature-card {
    position: relative;
    .featured-img {
      display: block;
      width: 100%;
      height: 300px;
      object-fit: cover;
      position: relative;
      z-index: 0;
    }
    .detail {
      position: absolute;
      left: 0;
      right: 0;
      bottom: 0;
      background-color: rgba(0, 0, 0, 0.6);
      padding: 16px;
      z-index: 1;
      h3 {
        color:#FFF;
        margin-bottom: 16px;
      }
      p {
        color: #FFF;
      }
    }
  }
  .movies-list {
    display: flex;
    flex-wrap: wrap;
    margin: 0px 8px;
    .movie {
      max-width: 25%;
      flex: 1 1 50%;
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
            background-color: #42B883;
            color: #FFF;
            bottom: 16px;
            left: 0px;
            text-transform: capitalize;
          }
        }
        .detail {
          background-color: #496583;
          padding: 16px 8px;
          flex: 1 1 100%;
          border-radius: 0px 0px 8px 8px;
          .year {
            color: #AAA;
            font-size: 14px;
          }
          h3 {
            color: #FFF;
            font-weight: 600;
            font-size: 18px;
          }
        }
      }
    }
  }
  section.new_index {
    min-height:300px;
    height:calc(500vh / 2.5);
    max-height:360px;
    background-position:top center;
    background-size:cover;
    background-image: url("https://www.themoviedb.org/t/p/w1920_and_h600_multi_faces_filter(duotone,032541,01b4e4)/r2NcIZ1FPMlxCty3vRITVTgGNVS.jpg");
    background-repeat:no-repeat;
  }
  @media only screen and (min-width: 1400px) {
    html {
      --maxPrimaryPageWidth: 1300px
    }
  }
  div.media.discover div.content_wrapper>div.title h2 {
    font-size:4em;
    color: white;
    font-weight:700;
    font-family: Arial, Helvetica, sans-serif;
    line-height:1;
  }
  section.new_index h3 {
    font-size:3em;
    font-weight:800;
    font-family: "Bradley Hand ITC";
    margin:5px;
    color: white;
  }
  section.new_index div.media {
    height:100%;
    display:flex;
    align-content:center;
    align-items:center;
    justify-content:center
  }
  section.new_index form {
    margin-top:30px;
    position:relative;
    top:0;
    left:0
  }
  section.new_index form input[type=text] {
    width:100%;
    height:46px;
    line-height:46px;
    font-size:1.1em;
    color:rgba(0,0,0,0.5);
    border:none;
    border-radius:30px;
    padding:10px 20px
  }
  section.new_index form input[type=text]:focus {
    outline:none
  }
  section.new_index form input[type=submit] {
    display:inline-flex;
    justify-content:center;
    align-content:center;
    align-items:center;
    height:46px;
    padding:10px 26px;
    border:none;
    background-image: linear-gradient(to right top, #d16ba5, #c777b9, #ba83ca, #aa8fd8, #9a9ae1, #8aa7ec, #79b3f4, #69bff8, #52cffe, #41dfff, #46eefa, #5ffbf1);
    border-radius:30px;
    position:absolute;
    top:0;
    font-weight: bold;
    font-size: 15px;
    right:-1px;
    color:black;
  }
  section.new_index form input[type=submit]:hover {
    color:white;
  }

}
body {
  background-color: lightcyan;
  height: inherit;
}

</style>