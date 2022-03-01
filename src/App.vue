<template>
  <div id="app">
      <MyHeader @textEnteredEvt="getTitles"/>
      <!--<PageLoading v-if="movieList==0" />-->
      <MyMain :movieList="movieList" :TVList="TVList"/>
      
  </div>
</template>

<script>
const axios = require('axios');


import MyHeader from './components/MyHeader.vue'
import MyMain from './components/MyMain.vue'
//import PageLoading from './components/PageLoading.vue';


export default {
  name: 'App',
  components: {
    MyHeader,
    MyMain,
 
  },
  data() {
    return {
      movieList: [],
      TVList: [],
      movieID: {},
      tvID: {},
      //movieCast: [],
      //TVCast: [],
      //results: [],
      api_key: '96259ec6f4490ebbbfaa7d8faba469f1',
      language: 'en-US',
    }
  },
  methods: {
    getTitles(keyword) {

      const params = {
        params: {
          'api_key': this.api_key,
          'query': keyword,
          'language': this.language
        }
      }
      // Make a request for a user with a given ID
      axios.all([
        //this syntax allows me to make several requests simultaneously
        axios.get('https://api.themoviedb.org/3/search/movie/', params),
        axios.get('https://api.themoviedb.org/3/search/tv', params),
        //axios.get('https://api.themoviedb.org/3/movie/'+ this.movieID + '/credits?api_key='+ this.api_key +'&language='+ this.language),
        //axios.get('https://api.themoviedb.org/3/tv/'+ this.tvID + '/credits?api_key='+ this.api_key +'&language='+ this.language)
      ])
        //by differentiating the different responses, I'm able to keep both lists separate
      .then(axios.spread((response1, response2) => {
          this.movieList = response1.data.results;
          this.movieID = response1.data.results.id;
          console.log(this.movieID)
          
          this.TVList = response2.data.results;
          this.tvID = response2.data.results.id;
          console.log(this.tvID)
          
          /*this.movieCast = response3.data.cast;
          console.log(this.movieCast)
          
          this.TVCast = response4.data.cast;
          console.log(this.TVCast)*/


          //I can combine the lists like this which will feed into the "results" array in data
          //this.results = [...this.movieList, ...this.TVList]

      }))
      .catch(function (error) {
      // handle error
      console.log(error);
      })
      .then(function () {

      });

      }
    }, 
    /*getCast() {
      axios.all([
        //this syntax allows me to make several requests simultaneously
        axios.get('https://api.themoviedb.org/3/movie/'+ this.movieID + '/credits?api_key='+ this.api_key +'&language='+ this.language),
        axios.get('https://api.themoviedb.org/3/tv/'+ this.tvID + '/credits?api_key='+ this.api_key +'&language='+ this.language)
      ])
        //by differentiating the different responses, I'm able to keep both lists separate
      .then(axios.spread((response1, response2) => {
          this.movieCast = response1.data.cast;
          this.TVCast = response2.data.cast;
          //I can combine the lists like this which will feed into the "results" array in data
          //this.results = [...this.movieList, ...this.TVList]
          console.log('movie cast' + this.movieCast);
          console.log('TV cast' + this.TVCast);

      }))
      .catch(function (error) {
      // handle error
      console.log(error);
      })
      .then(function () {

      });

    }*/  
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
