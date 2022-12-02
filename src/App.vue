<template>
  <h1>Pokemon Type Distribution</h1>
  <div id="app">
    <Table />
  </div>
  <p>Using pokeapi</p>
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
</style>
