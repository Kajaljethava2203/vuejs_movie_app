<template>

  <div class="row" style="text-align: justify;">
    <div class="column left" style="margin-left: 10px;">
      <div class="movie-img">
        <img :src="'https://image.tmdb.org/t/p/w500'+movie.backdrop_path"  alt="Movie Poster" class="featured-img" />
      </div>
    </div>
    <div class="column right">
      <div class="movie-detail">
        <h1 class="title">{{ movie.title }}</h1>
        <h2>Released Year : {{  new Date(movie.release_date).getFullYear()  }}</h2><br>
        <h3>
          <span v-for="genres in movie.genres" :key="genres"> {{genres.name}}, </span>
        </h3><br>
        <div class="plot">
          <h2>Overview</h2><br>
          <p>{{movie.overview}}</p><br>
        </div>
        <p><strong>Runtime : </strong> {{ (movie.runtime/60).toFixed(2)}} Hour</p><br>
        <p><strong>Tagline : </strong> {{movie.tagline}}</p><br>

      </div>
    </div>
  </div>

</template>
<script>
import {ref,onBeforeMount} from 'vue';
import {useRoute} from 'vue-router';
import env from "../env";
export default {
  setup(){
    const movie = ref([]);
    const route = useRoute();
    onBeforeMount(() => {
      fetch(`https://api.themoviedb.org/3/movie/${route.params.id}?api_key=${env.apikey}&language=en-US&append_to_response=credits`)
          .then(res => res.json())
          .then(res => {
            console.log(res);
            movie.value = res;
          });
    });

    return{
      movie,
      route
    }
  }

}
</script>
<style lang="scss">
.movie-detail {
  padding: 16px;
  h1 {
    color: Black;
    font-size: 35px;
    font-weight: 900;
    margin-bottom: 16px;
  }
  .featured-img {
    display: block;
    max-width: 400px;
    margin-bottom: 16px;
    padding-top: 50px;
  }
  p {
    color: black;
    font-size: 20px;
    line-height: 1.4;
  }
}
.column {
  float: left;
  padding: 10px;
  height: 300px;
}

.left {
  width: 25%;
}

.right {
  width: 75%;
  padding: 50px;
}

.row:after {
  content: "";
  display: table;
  clear: both;
}
.movie-img
{
  justify-content: center;
  padding: 45px;
}

</style>