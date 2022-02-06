<template>
  <div id="app">
    <Header />
    <Main />
  </div>
</template>

<script>
  import Header from './components/Header.vue';
  import Main from './components/Main.vue';

  export default {
    name: 'App',
    components: {
      Header,
      Main
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