<template>
    <div class="container"> 
        <div class="row">
            <h1>Movie Results</h1>
            <ul>
                <!-- v-for gets completed on app.vue once all $emits and props are properly identified throughout files-->
                <!-- using {{}} here takes each given object from the array and prints it on the screen -->
                    <!--:movies="movieList"  -->
                <MovieCard :movieList="movieList" :movie="movie"   
                v-for= "(movie, index) in movieList" :key= "index"/>
            </ul>
            <h1>TV Series Results</h1>
            <ul>
                <TVCard :TVList="TVList" :TVSeries="TVSeries"
                v-for= "(TVSeries, index1) in TVList" :key= "index1"/>
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