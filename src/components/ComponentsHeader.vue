
<script>
import axios from 'axios';
import { store } from '../store.js'

export default {
    name: 'ComponentsHeader',

    data(){
        return{
            store,
            apiKey:'77e03a919accfe25ba10020264bae0f0',
            apiUri: 'https://api.themoviedb.org/3/search/movie'
        }
    },

    methods: {
        getMovies(){
            //chiamata API
            axios.get(this.apiUri, {
                params : {
                    'api_key' : this.apiKey,
                    query : 'Witcher'
                }
            })
            .then(function (response) {
                console.log(response)
            })
            .catch(function(error){
                console.warn(error)
            });
        }
    },

    created(){
        this.getMovies();
    },
}
</script>

<template>
    <header>
        <label for="use-searchbar">
            insert your query:
        </label>
        <input type="text" id="use-searchbar">
        <button>Search</button>
    </header>
</template>

<style lang="scss">
    button{
        margin-left: 1rem;
    }
</style>