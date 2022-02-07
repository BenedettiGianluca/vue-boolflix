<template>
  <div id="app">
    <Header @search="ricercaFilmSerie"/>
    <Main />
  </div>
</template>

<script>
  import axios from 'axios';
  import Header from './components/Header.vue';
  import Main from './components/Main.vue';

  export default {
    name: 'App',
    components: {
      Header,
      Main
    },
    data(){
      return {
        apiMoviesURL: 'https://api.themoviedb.org/3/search/movie',
        apiSeriesURL: 'https://api.themoviedb.org/3/search/tv',
        films: [],
        series: []
      }
    },
    methods: {
      ricercaFilmSerie: function(nomeFilmSerie){
        let filtroRicerca = nomeFilmSerie;

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
  * {
    box-sizing: border-box;
    border: 0;
    margin: 0;
    background-color: #3C5064;
  }
</style>