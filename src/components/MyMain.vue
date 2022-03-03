<template>
    <div class="container"> 
        <div class="row">
            <div class="col">
                <h1>Movie Results</h1>
                <div class="row">
                    <!-- v-for on MyMain cycles through the array and provides the data from each individual movie -->
                    <MovieInfo :movieIDList="movieIDList" :movieList="movieList" :movie="movie"
                    v-for= "(movie, spindex) in movieList" :key= "spindex" />
                </div>
            </div>
        </div>
        <div class="row">
            <div class="col">
            <h1>TV Series Results</h1>
                <div class="row">
                    <TVInfo  :TVList="TVList" :TVSeries="TVSeries"
                    v-for= "(TVSeries, index) in TVList" :key= "index" />
                </div>
            </div>
        </div>
        <div class="row">
            <div class="col">
            <h1>TV Credits Results</h1>
                <div class="row" >
                    <TVCredits  :TVList="TVList" :TVSeries="TVSeries" :tvIDList="tvIDList" :tvID="tvID" 
                    v-for= "(tvID, index) in tvIDList" :key= "index" />
                </div>
            </div>
        </div>
        <div class="row">
            <div class="col">
            <h1>Movie Credits Results</h1>
                <div class="row">
                    <MovieCredits :movieList="movieList" :movie="movie" :movieIDList="movieIDList" :movieID="movieID"  
                    v-for= "(movieID, index) in movieIDList" :key= "index" />
                </div>
            </div>
        </div>
    </div>
</template>

<script>
const axios = require('axios');


import MovieInfo from './partials/MovieInfo.vue'
import TVInfo from './partials/TVInfo.vue'
import TVCredits from './partials/TVCredits.vue'
import MovieCredits from './partials/MovieCredits.vue'

export default {
    name: 'MyMain',
    components: {
        MovieInfo,    
        TVInfo,
        TVCredits,
        MovieCredits
    },
    data(){
        return {
            castList: [],
            actorsNames: [],
            api_key: '96259ec6f4490ebbbfaa7d8faba469f1',
            language: 'en-US',
        }
    },
    props: {
        'movieList': Array,
        'TVList': Array,
        'movieIDList': Array,
        'tvIDList': Array,
        //'tvID': Number,
        //'movieCast': Array,
        //'rating': Array,      
        //'movie': Object,
    },  
    mounted() {
        this.getCast();
    },
    methods: {
            getCast() {
                // Make a request for a user with a given ID
                axios.get('https://api.themoviedb.org/3/movie/'+ this.movieID + '/credits?api_key='+ this.api_key + '&language=' + this.language)
                .then((response) => {
                    this.castList = response.data.cast;
                    console.log(this.castList)

                    for(this.i=0;this.i<5;this.i++){
                    this.actorsNames.push(this.castList[this.i].name);
                    console.log(this.actorsNames)
                    }

                })
                .catch(function (error) {
                    // handle error
                    console.log(error);
                });
            }
        
    },

 

}
</script>

<style lang="scss">

@import '../style/general.scss';

.container {
    color: #fff;
    width: 80%;
    margin: auto;


    .my_card {
        height: 340px;
        width: 200px;
    }

}

</style>