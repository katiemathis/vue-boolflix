<template>
        <li class="TVSeries">
            <div>
                <div v-if="TVSeries.poster_path==null">{{TVSeries.name}}</div>
                <div v-else><img :src= "'http://image.tmdb.org/t/p/w154/' + TVSeries.poster_path" :alt="TVSeries.name"></div>
            </div>
            <div>{{TVSeries.name}}</div>
            <div>{{TVSeries.original_name}}</div>
            <div v-if= "TVSeries.original_language==''">{{TVSeries.original_language}}</div>
            <div v-else><lang-flag :iso= "TVSeries.original_language" /></div>
            <div>{{TVSeries.vote_average}}</div>
        </li>
</template>

<script>
import LangFlag from 'vue-lang-code-flags';
export default {
    name: 'TVCard',
    components: {
        LangFlag,
    },
    props: {
        'TVList': Array,
        'TVSeries': Object,
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

.TVSeries {
    width: 100%;
    list-style-type: none;
    background-color: $colorBackground;
}


</style>