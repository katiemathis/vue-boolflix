<template>
    <div class="container"> 
        <div class="row">
            <div class="col">
                <h1>Movie Results</h1>
                <div class="row">
                    <!-- v-for on MyMain cycles through the array and provides the data from each individual movie -->
                    <MovieInfo :movieList="movieList" :movie="movie"  
                    v-for= "(movie, index) in movieList" :key= "index"/>
                </div>
            </div>
        </div>
        <div class="row">
            <div class="col">
            <h1>TV Series Results</h1>
                <div class="row">
                    <TVInfo :TVList="TVList" :TVSeries="TVSeries"  
                    v-for= "(TVSeries, index) in TVList" :key= "index"
                    />
                </div>
            </div>
        </div>
    </div>
</template>

<script>
//const axios = require('axios');


import MovieInfo from './partials/MovieInfo.vue'
import TVInfo from './partials/TVInfo.vue'

export default {
    name: 'MyMain',
    components: {
        MovieInfo,    
        TVInfo,
    },
    props: {
        'movieList': Array,
        'TVList': Array,
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