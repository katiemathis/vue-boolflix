<template>
    <div class="container">
        <ul>
            <li>{{movieDetails}}</li>
            <li>TITOLO</li>
            <li>TITOLO ORIGINALE</li>
            <li>LINGUA</li>
            <li>VOTO</li>
        </ul>
    </div>
</template>

<script>
const axios = require('axios');

export default {
    name: 'MyMain',

    data () {
        return {
            movieDetails: [],
        }
    },
    methods: {
        getMovies() {
                // Make a request to get details from API
                axios
                .get('https://api.themoviedb.org/3/search/movie?api_key=96259ec6f4490ebbbfaa7d8faba469f1&language=en-US&query=joker&page=1&include_adult=false')
                .then((response) => {
                    this.movieDetails = response.data.results;
                    
                })                
                .catch(function (error) {
                    // handle error
                    console.log(error);
                });
        },
        /*mounted() {
            /*document.onreadystatechanges = () => {
                if (document.readyState == "complete") {
                    this.isloaded = true;
                }
            }
        },*/
        // complete the function (movie details list) upon reload of the page
        created() {
            this.getMovies();
            //this.isLoaded = true;
            console.log(this.getMovies)
       
        },
    },
    
}
</script>

<style lang="scss">

@import '../style/general.scss';

</style>