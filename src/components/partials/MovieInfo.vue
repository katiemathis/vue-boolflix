<template>
<!-- I created Movie Info which feeds into MyCard (with both movie and TV Info) to simplify css code and not duplicate -->
        <div class="movies col">
            <MyCard :movieList="movieList" :info="movie" :movieIDList="movieIDList" :movieID="movieID"/>
            <!--v-for="(movieID, index) in movieIDList" :key="index"-->
        </div>
</template>

<script>
import MyCard from './MyCard.vue'
//const axios = require('axios');

export default {
    name: 'MovieInfo',
    components: {
        MyCard,
    },
    //carrying this data over from MovieCredits to streamline -- might have to go directly into "MyCard"
    /*data(){
        return {
            castList: [],
            actorsNames: [],
            api_key: '96259ec6f4490ebbbfaa7d8faba469f1',
            language: 'en-US',
            actor: '',
        }
    },*/
    props: {
        'movieList': Array,
        'movie': Object,
        'movieIDList': Array,
        'movieID': Number,
    }, 
    /*mounted() {
        this.getCast() 
        //return this.actorsNames
            
    },
    methods: {
            getCast() {
                // Make a request for a user with a given ID
                axios.get('https://api.themoviedb.org/3/movie/'+ this.movieID + '/credits?api_key='+ this.api_key + '&language=' + this.language)
                .then((response) => {
                    this.castList = response.data.cast;
                    console.log(this.castList)

                    for(this.i=0;this.i<5;this.i++){
                    this.actorsNames.push(this.castList[this.i].name);
                    console.log(this.actorsNames)
                    }
                    return this.actorsNames;

                })
                .catch(function (error) {
                    // handle error
                    console.log(error);
                })
                .then(function () {

                });
            },
            
        },*/


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