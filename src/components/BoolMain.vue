<template>
    <main>
        <BoolHeader @filterChanged="serverCall"/>

        <ul class="film-wrapper">
            <h3>Movies</h3>
             <li v-for="el in moviesList" :key="el.id">
                 <figure class="img-wrapper">
                     <img :src="thumbnailUrl+thumbnailDimention.medium+checkBackDrop(el.backdrop_path)" alt="">
                 </figure>
                 <p>{{el.title}}</p>
                 <p>{{el.original_title}}</p>
                 <!-- <p>{{el.original_language}}</p> -->
                 <p>{{movieVote(el.vote_average)}} 
                     <span v-for="num in 5" :key="num"> 
                         <i :class="[num <= movieVote(el.vote_average) ? 'fa-solid fa-star' : 'fa-regular fa-star']"></i> 
                    </span>
                 </p>
                 <p>{{innerFlag(el.original_language)}}</p>
             </li>
        </ul>

        <ul class="series-wrapper">
            <h3>Series</h3>
             <li v-for="el in seriesList" :key="el.id">
                  <figure class="img-wrapper">
                     <img :src="thumbnailUrl+thumbnailDimention.medium+checkBackDrop(el.backdrop_path)" alt="">
                 </figure>
                 <p>{{el.name}}</p>
                 <p>{{el.original_name}}</p>
                 <!-- <p>{{el.original_language}}</p> -->
                 <p>{{el.vote_average}}</p>
                 <p>{{innerFlag(el.original_language)}}</p>
             </li>
        </ul>
    </main>
</template>

<script>
import BoolHeader from './BoolHeader.vue'
import getUnicodeFlagIcon from 'country-flag-icons/unicode'
import axios from 'axios'

export default {
    name:'BoolMain',
    data(){
        return{
            serverUrl: 'https://api.themoviedb.org/3',
            thumbnailUrl:'https://image.tmdb.org/t/p/',
            thumbnailDimention:{
                small: "w300",
                medium:"w780",
                large:"w1280",
                original:"original"
            },
            myKey: '720317410d2e858d6cb80c13e2f70aca',
            getMovies:'/search/movie',
            getSeries:'/search/tv',
            moviesList:[],
            seriesList:[]
        }
    },
    components:{
        BoolHeader
    },
    methods:{
        movieVote( originalVote ){
           return Math.ceil(originalVote / 2)
        },

        checkBackDrop( backDropPath ){
           return backDropPath ? backDropPath : '/qD7QAWEi5mUPyrhwWHoh9qfOliG.jpg'
        },

        //inserimento delle bandierine
        innerFlag( countryUnicode ){
            if( countryUnicode === 'en'){
                countryUnicode = 'GB'
            }
            return getUnicodeFlagIcon( countryUnicode.toUpperCase() )
        },     

        // chiamate al server
        serverCall( filter ){
            axios.get(`${this.serverUrl}${this.getMovies}`,{
                params: {
                    api_key: this.myKey,
                    query: filter
                }
            })
            .then( response => {
                console.log( response.data.results )
                this.moviesList = response.data.results
            } )
            .catch( err => {
                console.log(err.response)
            });

//--------------  CHIAMATA PER LE SEIRE TV  ------------------------------------------------
            axios.get(`${this.serverUrl}${this.getSeries}`,{
                params: {
                    api_key: this.myKey,
                    query: filter
                }
            })
            .then( response => {
                console.log( response.data.results )
                this.seriesList = response.data.results
            } )
            .catch( err => {
                console.log(err.response)
            })
        }
    },
}
</script>

<style lang="scss" scoped>
    main{
        background-color: cadetblue;
        height: 100vh;
        overflow-y: auto;

        ul{
            list-style: none;
            display: grid;
            grid-template-columns: repeat(5, 1fr);
            gap: 10px;

            // max-width: 80%;
            padding-inline: 20px;
            margin: 0 auto;
            margin-bottom: 20px;
            background-color: salmon;
            
            h3{
                grid-column: 1 / -1;
                color: white;
            }

            li{
                border: 2px solid red;
                // width: max-content;
                figure{
                    width: 100%;
                    aspect-ratio: 9/16;
                    img{
                        width: 100%;
                        height: 100%;
                        object-fit: cover;
                        object-position: center;
                    }
                }
                p{
                    margin-bottom: 5px;
                }
            }
        }
    }
</style>