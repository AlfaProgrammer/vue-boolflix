<template>
    <main>
        <BoolHeader @filterChanged="serverCall"/>
        <ul>
             <li v-for="el in moviesList" :key="el.id">
                 <p>{{el.title}}</p>
                 <p>{{el.original_title}}</p>
                 <p>{{el.original_language}}</p>
                 <p>{{el.vote_average}}</p>
             </li>
        </ul>
    </main>
</template>

<script>
import BoolHeader from './BoolHeader.vue'
import axios from 'axios'

export default {
    name:'BoolMain',
    data(){
        return{
            serverUrl: 'https://api.themoviedb.org/3',
            myKey: '720317410d2e858d6cb80c13e2f70aca',
            moviesList:[]
        }
    },
    components:{
        BoolHeader
    },
    methods:{       
        // chiamata al server
        serverCall( filter ){
            axios.get(`${this.serverUrl}/search/movie`,{
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

            max-width: 80%;
            padding-inline: 20px;
            margin: 0 auto;
            background-color: salmon;

            li{
                border: 2px solid red;
                p{

                }
            }
        }
    }
</style>