<template>
<!-- v-for gets completed on app.vue once all $emits and props are properly identified throughout files-->
<!-- using {{}} here takes each given object from the array and prints it on the screen -->
        <li class="TVSeries" >
            <div>
                <div v-if="TVSeries.poster_path==null">{{TVSeries.name}}</div>
                <div v-else><img :src= "'http://image.tmdb.org/t/p/w154/' + TVSeries.poster_path" :alt="TVSeries.name"></div>
            </div>
            <div>{{TVSeries.name}}</div>
            <div>{{TVSeries.original_name}}</div>
            <div v-if= "TVSeries.original_language==''">{{TVSeries.original_language}}</div>
            <div v-else><lang-flag :iso= "TVSeries.original_language" /></div>
            <div >{{fiveStarRating}}</div>
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
    data () {
        return {
            fiveStarRating: (Math.floor(this.TVSeries.vote_average))/2
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

.TVSeries {
    width: 100%;
    list-style-type: none;
    background-color: $colorBackground;
}


</style>