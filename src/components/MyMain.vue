<template>
    <div class="container"> 
        <div class="row">
            <h1>Movie Results</h1>
            <ul>
                <!-- v-for on MyMain cycles through the array and provides the data from each individual movie -->
                <MovieCard :movieList="movieList" :movie="movie"  
                v-for= "(movie, index) in movieList" :key= "index"/>
            </ul>
            <h1>TV Series Results</h1>
            <ul>
                <TVCard :TVList="TVList" :TVSeries="TVSeries"  
                v-for= "(TVSeries, index) in TVList" :key= "index"
                />
            </ul>
        </div>
    </div>
</template>

<script>
//const axios = require('axios');


import MovieCard from './partials/MovieCard.vue'
import TVCard from './partials/TVCard.vue'

export default {
    name: 'MyMain',
    components: {
        MovieCard,    
        TVCard,
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