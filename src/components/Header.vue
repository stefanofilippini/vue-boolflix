<template>
  <div class="header">
      <div class="header-image">
        <img src="../assets/Netflix-logo.png" alt="Netflix">
      </div>
      <ul class="nav">
          <li>
              <button>Home</button>
          </li>
          <li>
              <button>Film</button>
          </li>
          <li>
              <button>Serie TV</button>
          </li>
      </ul>
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
                return `https://api.themoviedb.org/3/search/movie?api_key=8051fb7b39a9d4b0ab49c690de6c3958&language=it-IT&query=${this.Text}`
            }
        },
        Api_tvSeries() {
            if (this.Text === "") {
                return ''
            } else {
                return `https://api.themoviedb.org/3/search/tv?api_key=8051fb7b39a9d4b0ab49c690de6c3958&language=it-IT&query=${this.Text}`
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
    .header {
        height: 80px;
        width: 100%;
        z-index: 1;
        background-color: black;
        display: flex;
        align-items: center;
        padding: 10px;
        position: fixed;
        top: 0;
        .header-image {
            display: flex;
            align-items: center;
            height: 100%;
            margin-right: 30px;
            img {
                height: 90%;
            }
        }
        .nav {
            display: flex;
            align-items: center;
            flex-grow: 1;
            list-style: none;
            li {
                margin-right: 20px;
                button {
                    background-color: transparent;
                    border: none;
                    text-transform: uppercase;
                    font-size: 18px;
                    color: rgb(190, 190, 190);
                    transition: 0,5s;
                    &:hover {
                        color: white;
                    }
                }
            }
        }
    }
    
</style>