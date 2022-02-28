<template>
    <div class="container"> 
        <div class="row">
            <ul>
                <!-- v-for gets completed on app.vue once all $emits and props are properly identified throughout files-->
                <!-- using {{}} here takes each given object from the array and prints it on the screen -->
                    <!--:movies="movieList"  -->
                <MovieCard :movieList="movieList" :movie="movie"   
                v-for= "(movie, index) in movieList" :key= "index"/>
            </ul>
        </div>
    </div>
</template>

<script>
//const axios = require('axios');


import MovieCard from './partials/MovieCard.vue'

export default {
    name: 'MyMain',
    components: {
        MovieCard,    
    },
    props: {
        'movieList': Array,
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