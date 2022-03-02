<template>
<!-- I created TVCast which will feeds into MyCard with tv credits info to simplify css code and not duplicate -->
        <div class="tv-series col">
           <MyCard :actor= "actor" :actorsNames= "actorsNames" v-for= "(actor, index) in actorsNames" :key= "index" />
        </div>
</template>

<script>
const axios = require('axios');

import MyCard from '../partials/MyCard.vue'
//import MyHeader from '../../components/MyHeader.vue'


export default {
    name: 'MovieCredits',
    components: {
        MyCard,
        
        
    },
    data(){
        return {
            castList: [],
            actorsNames: [],
            api_key: '96259ec6f4490ebbbfaa7d8faba469f1',
            language: 'en-US',
            actor: '',
        }
    },
    props: {
        'movieList': Array,
        'movie': Object,
        'movieIDList': Array,
        'movieID': Number,
        //'api_key': String,
        //'language': String,
    },
    mounted() {
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

                    //this.getCastNames();

                })
                .catch(function (error) {
                    // handle error
                    console.log(error);
                })
                .then(function () {

                });
            },
            
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

.debug-button {
    width: 100px;
    height: 50px;
}

.hide {
    display: none;
}



</style>