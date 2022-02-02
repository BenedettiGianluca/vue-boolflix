<template>
  <div id="app">
    <SearchBar />
  </div>
</template>

<script>
import SearchBar from './components/SearchBar.vue';

export default {
  name: 'App',
  components: {
    SearchBar
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