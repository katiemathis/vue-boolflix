<template>
    <!--<div v-if="loadingInProgress" class="main_container">
        <div class="container" >
            <PageLoading />
        </div>
    </div>-->
    <div class="container"> 
        <div class="row">
                <!-- v-for gets completed on app.vue once all $emits and props are properly identified throughout files-->
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