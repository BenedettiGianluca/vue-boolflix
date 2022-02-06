<template>
  <header class="header">
    <h1>BOOLFLIX</h1>
  </header>
</template>

<script>
  export default {
    name: 'Header'
  }
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
  }
</style>