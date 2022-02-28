<template>
        <li class="movies">
            <div>
                <div v-if="movie.poster_path==null">{{movie.title}}</div>
                <div v-else><img :src= "'http://image.tmdb.org/t/p/w154/' + movie.poster_path" :alt="movie.title"></div>
            </div>
            <div>{{movie.title}}</div>
            <div>{{movie.original_title}}</div>
            <div v-if= "movie.original_language==''">{{movie.original_language}}</div>
            <div v-else><lang-flag :iso= "movie.original_language" /></div>
            <div>{{movie.vote_average}}</div>
        </li>
</template>

<script>
import LangFlag from 'vue-lang-code-flags';
export default {
    name: 'MovieCard',
    components: {
        LangFlag,
    },
    props: {
        'movieList': Array,
        'movie': Object,
    }, 

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