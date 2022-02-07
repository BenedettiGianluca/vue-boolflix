<template>
  <header class="header">
    <h1>BOOLFLIX</h1>
    <input type="text" placeholder="Digita il nome di un film o di una serie tv" v-model="nomeFilmSerie" v-on:keyup.enter="$emit('search',nomeFilmSerie)">
  </header>
</template>

<script>
  export default {
    name: 'Header',
    data(){
      return {
        nomeFilmSerie: ""
      };
    }
  };
</script>

<style lang="scss">
  .header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    background-color: #5D5064;
    width: 100vw;
    heigth: 10vh;
    padding: 3vh 9vw;
    border-bottom: 6px solid #500800;

    h1 {
      background-color: #5D5064;
      color: #ffffee;
      font-size: 20px;
    }

    input {
      background-color: #500800;
      color: #33C933;
      height: 25px;
      width: 60vw;
      margin: 5vh 30px 4vh 200px;

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
  }
</style>