<template>
  <div class="searchBar">
    <input type="text" placeholder="Digita il nome di un film">
    <button type="button" @click="ricercaFilm">Cerca</button>
    <div class="filmTrovati">
      <div class="film" v-for="(element, index) in films" :key="index">
        <h2>Titolo: {{element.title}}</h2>
        <h3>Titolo originale: {{element.original_title}}</h3>
        <p>Lingua: {{element.original_language}}</p>
        <p>Voti: {{element.vote_count}}</p>
        <p>Valutazione: {{element.vote_average}}</p>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';   /* push di prova */

export default {
  name: 'SearchBar',
  data(){
    return {
      apiURL: 'https://api.themoviedb.org/3/search/movie',
      films: []
    }
  },
  methods: {
    ricercaFilm: function(){
      let filtroRicercaFilm = document.querySelector('.searchBar>input').value;
      axios
      .get(this.apiURL, {
        params: {
          api_key: '35c708968a77a980b6cd9af13310e62e',
          query: filtroRicercaFilm,
        },
      })
      .then(risposta => {
        this.films = risposta.data.results
      })
      .catch(function (error) {
        console.log(error);
      })
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

    .filmTrovati {
      display: flex;
      flex-wrap: wrap;
      justify-content: center;
      align-items: flex-start;
      height: 60vh;
      padding: 30px;
      margin: 0 50px;

      .film {
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        padding: 30px;
        margin: 30px;

        h2, h3, p {
          color: #ffffee;
          padding: 10px 0;
        }
      }
    }
  }
</style>