<template>
    <div class="container"> 
        <div class="row">
            <div class="col">
                <h1>Movie Results</h1>
                <div class="row">
                    <!-- v-for on MyMain cycles through the array and provides the data from each individual movie -->
                    <MovieInfo :movieIDList="movieIDList" :movieList="movieList" 
                    :movie="movie" :movieID="movieID"
                    v-for= "(movie, spindex) in movieList" :key= "spindex" />
                    <!--<MovieCredits :movieIDList="movieIDList" :movieID="movieID" 
                    v-for= "(movieID, index) in movieIDList" :key= "index"/>-->
                </div>
            </div>
        </div>
        <div class="row">
            <div class="col">
            <h1>TV Series Results</h1>
                <div class="row">
                    <TVInfo  :TVList="TVList" :TVSeries="TVSeries"
                    v-for= "(TVSeries, pindex) in TVList" :key= "pindex" />
                </div>
            </div>
        </div>
        <div class="row">
            <div class="col">
            <h1>TV Credits Results</h1>
                <div class="row">
                    <TVCredits  :tvIDList="tvIDList" :tvID="tvID" 
                    v-for= "(tvID, skindex) in tvIDList" :key= "skindex" />
                </div>
            </div>
        </div>
        <!--<div class="row">
            <div class="col">
            <h1>Movie Credits Results</h1>
                <div class="row">
                    <MovieCredits  :movieIDList="movieIDList" :movieID="movieID" 
                    v-for= "(movieID, index) in movieIDList" :key= "index" />
                </div>
            </div>
        </div>-->
    </div>
</template>

<script>
//const axios = require('axios');


import MovieInfo from './partials/MovieInfo.vue'
import TVInfo from './partials/TVInfo.vue'
import TVCredits from './partials/TVCredits.vue'
//import MovieCredits from './partials/MovieCredits.vue'

export default {
    name: 'MyMain',
    components: {
        MovieInfo,    
        TVInfo,
        TVCredits,
        //MovieCredits
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