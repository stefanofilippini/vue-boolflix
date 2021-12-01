<template>
    <div>
        <ul class="card-list">
            <li class="card" v-for="(card, i) in CardList" :key="`card-${i}`">
                <div><img class="card-image" :src="`https://image.tmdb.org/t/p/w500${card.poster_path}`" :alt="card.original_title ? card.original_title : card.original_name"></div>
                <div>{{ card.title ? card.title : card.name }}</div>
                <div>{{ card.original_title ? card.original_title : card.original_name }}</div>
                <div v-if="languages.includes(card.original_language)"><img class="flag" :src="require(`../assets/${card.original_language}.png`)" :alt="card.original_language"></div>
                <div v-else>{{ card.original_language }}</div>
                <div>{{ card.vote_average }} </div>
            </li>
        </ul>
    </div>  
</template>

<script>
export default {
    
    name: 'CardList',

    data() {
        return {
        languages: ['it', 'en', 'de'],
        }
    },

    props: {
        CardList: Array,
    }


}
</script>

<style scoped lang="scss">
    .card-list {
        display: flex;
        flex-wrap: wrap;
        list-style: none;
        justify-content: space-around;
        align-items: center;
        .card {
            width: calc((100% / 4) - 10px);
            border: 1px solid black;
            padding: 10px;
            .card-image {
                width: 100%;
            }
            .flag {
                width: 50px;
            }
        }
    }
</style>