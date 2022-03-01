<template>
<!-- I created TVInfo which feeds into MyCard (with both movie and TV Info) to simplify css code and not duplicate -->
        <div class="tv-series col">
            <MyCard :TVList="TVList" :info="TVSeries" />
            
             

        </div>
</template>

<script>

import MyCard from '../partials/MyCard.vue'


export default {
    name: 'TVInfo',
    components: {
        MyCard,
    },
    props: {
        'TVList': Array,
        'TVSeries': Object,
        //'tvIDList': Array,
        //'tvID': Number
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