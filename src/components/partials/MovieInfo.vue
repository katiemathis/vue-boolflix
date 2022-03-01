<template>
<!-- I created Movie Info which feeds into MyCard (with both movie and TV Info) to simplify css code and not duplicate -->
        <div class="movies col">
            <MyCard :movieList="movieList" :info="movie" />
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