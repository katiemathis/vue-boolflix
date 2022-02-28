<template>
  <div id="app">
      <MyHeader @textEnteredEvt="getMovies"/>
      <PageLoading v-if="movieList==0" />
      <MyMain v-else
      :movieList="movieList" :movie="movie"    
      v-for= "(movie, index) in movieList" :key= "index"
      />
      <!-- v-for on MyMain cycles through the array and provides the data from each individual movie -->
  </div>
</template>

<script>
const axios = require('axios');

import MyHeader from './components/MyHeader.vue'
import MyMain from './components/MyMain.vue'
import PageLoading from './components/PageLoading.vue';


export default {
  name: 'App',
  components: {
    MyHeader,
    MyMain,
    PageLoading,
 
  },
  data() {
    return {
      movieList: [],
      api_key: '96259ec6f4490ebbbfaa7d8faba469f1',
      language: 'en-US',
    }
  },
  methods: {
    getMovies(keyword) {
                // Make a request for a user with a given ID
                axios.get('https://api.themoviedb.org/3/search/movie?api_key='+ this.api_key +'&query='+ keyword +'&language='+ this.language +'&include_adult=false')
                .then((response) => {
                    this.movieList = response.data.results;
                    //this.loadingInProgress = false;
                })
                .catch(function (error) {
                    // handle error
                    console.log(error);
                })
                .then(function () {

                });

            }
        },   
  }

</script>

<style scoped lang="scss">

@import './style/general.scss';

*{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  background-color: $colorBackground;

}

#app {
  width: 100%;
  height: 100%;
  /*font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;*/
}
</style>
