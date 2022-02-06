<template>
  <div class="searchBar">
    <input type="text" placeholder="Digita il nome di un film o di una serie tv">
    <button type="button" @click="ricerca">Cerca</button>
    <div class="filmSerieTrovati">
      <div class="film" v-for="(element, filmsIndex) in films" :key="filmsIndex">
        <img :src="`https://image.tmdb.org/t/p/w342${element.poster_path}`">
        <h2>Titolo: {{element.title}}</h2>
        <h3>Titolo originale: {{element.original_title}}</h3>
        <p>Lingua: <span v-if="((element.original_language!='it')&&(element.original_language!='en')&&(element.original_language!='fr'))">non specificata</span>
          <img v-if="(element.original_language=='it')" src="https://7laghikartitalia.it/wp-content/uploads/Bandiera-d-Italia-1920x1080.jpg">
          <img v-if="(element.original_language=='en')" src="https://besthqwallpapers.com/Uploads/26-5-2019/94067/thumb2-flag-of-united-kingdom-4k-stone-background-grunge-flag-europe.jpg">
          <img v-if="(element.original_language=='fr')" src="https://p4.wallpaperbetter.com/wallpaper/824/310/435/flags-flag-of-france-wallpaper-preview.jpg">
        </p>
        <p>Voti: {{element.vote_count}}</p>
        <p class="stelle">Valutazione: 
          <i v-if="Math.ceil(element.vote_average/2)>=1" class="fas fa-star"></i>
          <i v-if="Math.ceil(element.vote_average/2)>=2" class="fas fa-star"></i>
          <i v-if="Math.ceil(element.vote_average/2)>=3" class="fas fa-star"></i>
          <i v-if="Math.ceil(element.vote_average/2)>=4" class="fas fa-star"></i>
          <i v-if="Math.ceil(element.vote_average/2)>=5" class="fas fa-star"></i>
        </p>
      </div>
      <div class="tvShow" v-for="(element, seriesIndex) in series" :key="seriesIndex">
        <img :src="`https://image.tmdb.org/t/p/w342${element.poster_path}`">
        <h2>Titolo: {{element.name}}</h2>
        <h3>Titolo originale: {{element.original_name}}</h3>
        <p>Lingua: <span v-if="((element.original_language!='it')&&(element.original_language!='en')&&(element.original_language!='fr'))">non specificata</span>
          <img v-if="(element.original_language=='it')" src="https://7laghikartitalia.it/wp-content/uploads/Bandiera-d-Italia-1920x1080.jpg">
          <img v-if="(element.original_language=='en')" src="https://besthqwallpapers.com/Uploads/26-5-2019/94067/thumb2-flag-of-united-kingdom-4k-stone-background-grunge-flag-europe.jpg">
          <img v-if="(element.original_language=='fr')" src="https://p4.wallpaperbetter.com/wallpaper/824/310/435/flags-flag-of-france-wallpaper-preview.jpg">
        </p>
        <p>Voti: {{element.vote_count}}</p>
        <p class="stelle">Valutazione: 
          <i v-if="Math.ceil(element.vote_average/2)>=1" class="fas fa-star"></i>
          <i v-if="Math.ceil(element.vote_average/2)>=2" class="fas fa-star"></i>
          <i v-if="Math.ceil(element.vote_average/2)>=3" class="fas fa-star"></i>
          <i v-if="Math.ceil(element.vote_average/2)>=4" class="fas fa-star"></i>
          <i v-if="Math.ceil(element.vote_average/2)>=5" class="fas fa-star"></i>
        </p>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'SearchBar',
  data(){
    return {
      apiMoviesURL: 'https://api.themoviedb.org/3/search/movie',
      apiSeriesURL: 'https://api.themoviedb.org/3/search/tv',
      films: [],
      series: []
    }
  },
  methods: {
    ricerca: function(){
      let filtroRicerca = document.querySelector('.searchBar>input').value;
      axios
      .get(this.apiMoviesURL, {
        params: {
          api_key: '35c708968a77a980b6cd9af13310e62e',
          query: filtroRicerca,
        },
      })
      .then(risposta => {
        this.films = risposta.data.results;
      })
      .catch(function (error) {
        console.log(error);
      });

      axios
      .get(this.apiSeriesURL, {
        params: {
          api_key: '35c708968a77a980b6cd9af13310e62e',
          query: filtroRicerca,
        },
      })
      .then(risposta => {
        this.series = risposta.data.results;
      })
      .catch(function (error) {
        console.log(error);
      });
    }
  }
}
</script>

<style lang="scss">
  .searchBar {
    margin-top: 10vh;

    input {
      background-color: #500800;
      color: #33C933;
      height: 25px;
      width: 60vw;
      margin: 0 30px 5vh 200px;

      &::placeholder {
        color: #219621;
        opacity: 1;
      }
      &:-ms-input-placeholder {
        color: #219621;
      }
      &::-ms-input-placeholder {
        color: #219621;
      }
    }

    button {
      background-color: #500800;
      color: #33C933;
      padding: 5px;
    }

    .filmSerieTrovati {
      display: flex;
      flex-wrap: wrap;
      justify-content: center;
      align-items: flex-start;
      height: 60vh;
      padding: 30px;
      margin: 0 50px;

      .film, .tvShow {
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        padding: 30px;
        margin: 30px;

        h2, h3, p {
          color: #ffffee;
          padding: 10px 0;

          img {
            height: 18px;
            width: 24px;
          }

          .fa-star {
            color: yellow;
          }
        }
      }
    }
  }
</style>