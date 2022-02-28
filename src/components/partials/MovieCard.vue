<template>
        <div class="movies col">
            <div class="row row-cols-lg-4 row-cols-md-2 row-cols-1">
                <div>
                    <div v-if="movie.poster_path==null">{{movie.title}}</div>
                    <div v-else><img :src= "'http://image.tmdb.org/t/p/w154/' + movie.poster_path" :alt="movie.title"></div>
                </div>
                <!--<div>{{movie.title}}</div>
                <div>{{movie.original_title}}</div>
                <div v-if= "movie.original_language==''">{{movie.original_language}}</div>
                <div v-else><lang-flag :iso= "movie.original_language" /></div>
                <div>
                    <i class="fa-solid fa-star" v-for="(rating, index) in fiveStarRating" :key="index"></i>
                    <i class="fa-solid fa-star-half" v-for="(rating, index) in fiveStarRating%1" :key="index"></i>
                </div>-->
            </div>
        </div>
</template>

<script>
//import LangFlag from 'vue-lang-code-flags';
export default {
    name: 'MovieCard',
    /*components: {
        LangFlag,
    },*/
    props: {
        'movieList': Array,
        'movie': Object,
    }, 
    data () {
        return {
            fiveStarRating: (Math.ceil(this.movie.vote_average))/2
        }
    } 

}
</script>

<style lang="scss">

@import '../../style/general.scss';

*{
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

.movies {
    width: 100%;
    list-style-type: none;
    background-color: $colorBackground;
}

</style>