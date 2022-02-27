<template>
    <!--<div v-if="loadingInProgress" class="main_container">
        <div class="container" >
            <PageLoading />
        </div>
    </div>-->
    <div class="container">
        <!-- v-for here cycles through the array and provides the data from each individual movie -->
        <!-- v-for="(movie, index) in movieList" :key="index" -->
        <div class="row" >
            <!-- using {{}} here takes each given object from the array and prints it on the screen -->
            <h3>Title: {{movie.title}}</h3>
            <ul>
                <li>Original Title: {{movie.original_title}}</li>
                <li>Original Language: {{movie.original_language}}</li>
                <li>Average Vote: {{movie.vote_average}}</li>
            </ul>
        </div>
    </div>
</template>

<script>
//const axios = require('axios');


//import PageLoading from './partials/PageLoading.vue'

export default {
    name: 'MyMain',
    props: {
        'movieList': Array,
        'movie': Object,
    },
    /*data () {
          return {
              movieList: [],
              loadingInProgress: true,
          }      
    },
    methods: {
            getMovies() {
                // Make a request for a user with a given ID
                axios.get('https://api.themoviedb.org/3/search/movie?api_key=96259ec6f4490ebbbfaa7d8faba469f1&language=en-US&query=joker&page=1&include_adult=false')
                .then((response) => {
                    this.movieList = response.data.results;
                    this.loadingInProgress = false;

                    /*this.cardItems.forEach(cardItem => {
                        if (!this.genreItems.includes(cardItem.genre)) {
                            this.genreItems.push(cardItem.genre);
                            console.log(this.genreItems)
                        }
                    });

                    this.$emit('genresReady', this.genreItems)
                    
                })
                .catch(function (error) {
                    // handle error
                    console.log(error);
                });
            }
        },
        /*mounted() {
            document.onreadystatechanges = () => {
                if (document.readyState == "complete") {
                    this.isloaded = true;
                }
            }
        },
        created() {
            this.getMovies();
            this.loadingInProgress = false;
            
        }*/
    
    
}
</script>

<style lang="scss">

@import '../style/general.scss';

.container {
    color: #fff;
    width: 80%;
    margin: auto;

}

</style>