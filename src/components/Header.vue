<template>
  <div class="header">
      <Form @searchText="reciveText"/>
      <ul v-for="(film, i) in Films" :key="`Film-${i}`">
            <li> {{ film.title }}</li>
            <li> {{ film.original_title }}</li>
            <li v-if="languages.includes(film.original_language)"><img :src="require(`../assets/${film.original_language}.png`)" :alt="film.original_language"></li>
            <li v-else>{{ film.original_language }}</li>
            <li> {{ film.vote_average }}</li>
      </ul>
  </div>
</template>

<script>

import Axios from 'axios';
import Form from '@/components/Form';

export default {
    name: 'Header',

    components: {
        Form,
    },

    data() {
        return {
        Films: [],
        Text: '',
        ApiSearch: '',
        languages: ['it', 'en'],
        }
    },

    computed: {
        Api() {
            if (this.Text === "") {
                return ''
            } else {
                return `https://api.themoviedb.org/3/search/movie?api_key=8051fb7b39a9d4b0ab49c690de6c3958&query=${this.Text}`
            }
        }
    },

    methods: {
        call_api_movie(Api) {
            Axios.get(Api)
            .then(result => this.Films = result.data.results)
            .catch(error => console.log(error));
        },

        reciveText(Text) {
            this.Text = Text;
            this.call_api_movie(this.Api)
        },
    }
}
</script>

<style scoped leng="scss">

</style>