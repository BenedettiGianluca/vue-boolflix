<template>
  <div class="searchBar">
    <input type="text" placeholder="Digita il nome di un film">
    <button type="button" @click="ricercaFilm">Cerca</button>
    <div class="filmTrovati">
      <div class="film" v-for="(element, index) in films" :key="index">
        <h1>{{element.title}}</h1>
        <h2>{{element.original_title}}</h2>
        <p>{{element.original_language}}</p>
        <p>{{element.vote_count}}</p>
        <p>{{element.vote_average}}</p>
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
      apiURL: 'https://api.themoviedb.org/3/search/movie?api_key=35c708968a77a980b6cd9af13310e62e&query=',
      films: []
    }
  },
  methods: {
    ricercaFilm: function(){
      filtroRicercaFilm: document.querySelector('.searchBar>input').value;
      apiURL: 'https://api.themoviedb.org/3/search/movie?api_key=35c708968a77a980b6cd9af13310e62e&query=' + filtroRicercaFilm;
      axios
      .get(this.apiURL)
      .then(risposta => {
        this.films = risposta.data.response
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
      margin: 0 50px 6vh 200px;

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
      justify-content: center;
      align-items: center;
      padding: 30px;
      margin: 0 100px;

      .film {
        display: flex;
        justify-content: center;
        align-items: center;
        padding: 30px;
        margin: 30px;
      }
    }
  }
</style>