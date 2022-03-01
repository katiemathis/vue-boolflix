<template>
<!-- I created Movie Info which feeds into MyCard (with both movie and TV Info) to simplify css code and not duplicate -->
        <div class="movies col">
            <MyCard :movieList="movieList" :info="movie" :IDList="movieIDList" :ID="movieID" />
            <!--v-for="(movieID, index) in movieIDList" :key="index"-->
        </div>
</template>

<script>
import MyCard from './MyCard.vue'

export default {
    name: 'MovieInfo',
    components: {
        MyCard,
    },
    props: {
        'movieList': Array,
        'movie': Object,
        'movieIDList': Array,
        'movieID': Number,


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



</style>