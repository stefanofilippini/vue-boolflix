<template>
  <div id="app">
    <Header @film="ReciveFilms" @series="ReciveSeries"/>
    <h1 v-show="Films.length != 0">Abbiamo trovato per te i seguenti film:</h1>
    <CardList :CardList="Films"/>
    <h1 v-show="tvSeries.length != 0">Abbiamo trovato per te le seguenti serie tv:</h1>
    <CardList :CardList="tvSeries"/>
  </div>
</template>

<script>
import Header from './components/Header.vue'
import CardList from './components/CardList.vue';

export default {
  name: 'App',

  data() {
        return {
        Films: [],
        tvSeries: [],
        }
    },

  components: {
    Header,
    CardList,
  },

  methods: {
    ReciveFilms(Array) {
            this.Films = Array;
        },
    ReciveSeries(Array) {
            this.tvSeries = Array;
        },
  }
}
</script>

<style lang="scss">
  *{
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    font-family: sans-serif;
  }

  body {
    background-color: #141414;
  }

  h1 {
    color: white;
    margin-left: 20px;
    margin-top: 30px;
    &:first-of-type {
      margin-top: 120px;
    }
  }
</style>
