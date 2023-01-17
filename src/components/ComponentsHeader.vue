
<script>
import axios from 'axios';
import { store } from '../store.js'


export default {
    name: 'ComponentsHeader',

    data(){
        return{
            store,
            apiKey:'77e03a919accfe25ba10020264bae0f0',
            apiUri: 'https://api.themoviedb.org/3/search/',
            flags: ['en', 'es', 'it', 'fr', 'ol', 'zh'],
        }
    },

    methods: {
        getMoviesSeries(apiSearch, searchQuery){
            //chiamata API
            axios.get(this.apiUri + apiSearch , {
                params : {
                    'api_key' : this.apiKey,
                    query : searchQuery
                }
            })
            .then( (response) => {
                console.log(response.data.results)
                console.log(response.data.results)
                if(apiSearch === 'movie'){
                    this.store.movies = response.data.results
                }else{
                    this.store.series = response.data.results
                }
            })
            .catch(function(error){
                console.warn(error)
            });
        },

        getMoviesAndSeriesTv(searchQuery){
            this.getMoviesSeries('movie', searchQuery)
            this.getMoviesSeries('tv', searchQuery)
        },
        getImagePath : function(imgPath){
            return new URL (`../assets/img/${imgPath}.webp`, import.meta.url).href
        }
    },

    created(){
    },

    computed:{
        moviesAndSeries(){
            return [...this.store.movies, ...this.store.series];
        }
    },

}

</script>

<template>
    <header>
        <label for="use-searchbar">
            insert your query:
        </label>
        <input type="text" id="use-searchbar" v-model="store.searchText">
        <button @click="getMoviesAndSeriesTv(store.searchText)">Search</button>
        <ul>
            <li v-for="movieElement in moviesAndSeries ">
                <h3>
                    {{ movieElement.title ? movieElement.title : movieElement.name }} 
                </h3>

                <h5>
                    {{ movieElement.original_title ? movieElement.original_title : movieElement.original_name }}
                </h5>

                <p>
                    Language: <img class="my-dimension" v-if="flags.includes(movieElement.original_language)" :src="getImagePath(movieElement.original_language)" alt="State">
                    <span v-else class="languages">
                        {{ movieElement.original_language }}
                    </span>
                    <br>
                    <span>
                Rating: <i v-for="star in 5" :key="star"
                        :class="(star < movieElement.vote_average / 2) ? 'fas fa-star' : 'far fa-star'"></i>
            </span>
                </p>    

                <p>
                    <img :src="`https://image.tmdb.org/t/p/w342${movieElement.poster_path}`" alt="">
                </p>
            </li>
        </ul>
    </header>
</template>

<style lang="scss">
    button{
        margin-left: 1rem;
    }

    .my-dimension{
        width: 20px;
    }
</style>