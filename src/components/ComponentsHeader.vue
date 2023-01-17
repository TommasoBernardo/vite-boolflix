
<script>
import axios from 'axios';
import { store } from '../store.js'


export default {
    name: 'ComponentsHeader',

    data(){
        return{
            store,
            apiKey:'77e03a919accfe25ba10020264bae0f0',
            apiUri: 'https://api.themoviedb.org/3/search/movie',
            flags: ['en', 'es', 'it', 'fr', 'ol', 'zh'],
        }
    },

    methods: {
        getMovies(searchQuery){
            //chiamata API
            axios.get(this.apiUri, {
                params : {
                    'api_key' : this.apiKey,
                    query : searchQuery
                }
            })
            .then( (response) => {
                console.log(response.data.results)
                this.store.movies = response.data.results;
            })
            .catch(function(error){
                console.warn(error)
            });
        },
        getImagePath : function(imgPath){
            return new URL (`../assets/img/${imgPath}.webp`, import.meta.url).href
        }
    },

    created(){
    },
    
}
</script>

<template>
    <header>
        <label for="use-searchbar">
            insert your query:
        </label>
        <input type="text" id="use-searchbar" v-model="store.searchText">
        <button @click="getMovies(store.searchText)">Search</button>
        <ul>
            <li v-for="movieElement in store.movies">
                <h3>
                    {{ movieElement.title }} 
                </h3>

                <h5>
                    {{ movieElement.original_title }}
                </h5>

                <p>
                    Language: <img v-if="flags.includes(movieElement.original_language)" :src="getImagePath(movieElement.original_language)" alt="State">
                    <span v-else class="languages">
                        {{ movieElement.original_language }}
                    </span>
                    <br>
                    rating:{{ movieElement.vote_average }} stars
                </p>

            </li>
        </ul>
    </header>
</template>

<style lang="scss">
    button{
        margin-left: 1rem;
    }

    img{
        width: 20px;
    }
</style>