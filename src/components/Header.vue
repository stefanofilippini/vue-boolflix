<template>
  <div class="header">
      <Form @searchText="reciveText"/>
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
        Text: '',
        Films: [],
        tvSeries: [],
        ApiSearch: '',
        languages: ['it', 'en'],
        }
    },

    computed: {
        Api_film() {
            if (this.Text === "") {
                return ''
            } else {
                return `https://api.themoviedb.org/3/search/movie?api_key=8051fb7b39a9d4b0ab49c690de6c3958&query=${this.Text}`
            }
        },
        Api_tvSeries() {
            if (this.Text === "") {
                return ''
            } else {
                return `https://api.themoviedb.org/3/search/tv?api_key=8051fb7b39a9d4b0ab49c690de6c3958&query=${this.Text}`
            }
        }
    },

    methods: {
        call_api_movie(Api) {
            Axios.get(Api)
            .then(result => {
                this.Films = result.data.results;
                this.$emit('film', this.Films);
            })
            .catch(error => console.log(error));
        },

        call_api_tvSeries(Api) {
            Axios.get(Api)
            .then(result => {
                this.tvSeries = result.data.results;
                this.$emit('series', this.tvSeries);
            })
            .catch(error => console.log(error));
        },

        reciveText(Text) {
            this.Text = Text;
            this.call_api_movie(this.Api_film)
            this.call_api_tvSeries(this.Api_tvSeries)
        },
    }
}
</script>

<style scoped lang="scss">
    
</style>