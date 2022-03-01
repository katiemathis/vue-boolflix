<template>
<!-- I created TVInfo which feeds into MyCard (with both movie and TV Info) to simplify css code and not duplicate -->
        <div class="tv-series col">
            <MyCard :TVList="TVList" :info="TVSeries" />

        </div>
</template>

<script>
import MyCard from '../partials/MyCard.vue'


export default {
    name: 'TVCard',
    components: {
        MyCard,
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



</style>