<template>
  <div id="app">
    <Header @film="ReciveFilms" @series="ReciveSeries"/>
    <CardList :CardList="Films"/>
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
</style>
