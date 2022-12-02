<template>
  <h1>Pokemon Type Distribution</h1>
  <div id="app">
    <Table />
  </div>
  <div class="footer">
    <p>
      This chart displays the number of pokemon of each type (Pokemon with dual
      types are counted for both types)
    </p>
    <p>Pokemon data collected using pokeapi.co</p>
    <p>Website made by JD Tramonte</p>
  </div>
</template>

<script>
import Table from './components/Table.vue';

import axios from 'axios';

export default {
  name: 'App',
  components: {
    Table,
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.footer {
  position: relative;
  bottom: 0;
  margin: auto;
}
</style>
