<template>
  <div id="app">
      <MyHeader @textEnteredEvt="getTitles"/>
      <!--<PageLoading v-if="movieList==0" />-->
      <MyMain :movieList="movieList" :TVList="TVList" :movieIDList="movieIDList" :tvIDList="tvIDList" :results="results"/>
      <!--v-for= "(movieID, index) in movieIDList" :key= "index"-->
      
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
      movieIDList: [],
      tvIDList: [],
      movieID: '',
      tvID: '',
      movieCast: [],
      TVCast: [],
      actorNames: [],
      ID: '',
      results: [],
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
          'language': this.language,
          'movie_ID': this.movieID,
          'tv_ID': this.tvID,

        }
      }
      // Make a request for a user with a given ID
      axios.all([
        //this syntax allows me to make several requests simultaneously
        axios.get('https://api.themoviedb.org/3/search/movie/', params),
        axios.get('https://api.themoviedb.org/3/search/tv', params),
        //axios.get('https://api.themoviedb.org/3/movie/876716/credits?api_key=' + this.api_key +'&language='+ this.language),
        //axios.get('https://api.themoviedb.org/3/tv/'+ this.tvID + '/credits?api_key='+ this.api_key + '&language=' + this.language)
      ])
        //by differentiating the different responses, I'm able to keep both lists separate
      .then(axios.spread((response1, response2) => {
          this.movieList = response1.data.results;
          this.TVList = response2.data.results;
          //this.movieCast = response3.data.cast;
          //console.log('movie cast' + this.movieCast)
          
          //this.TVCast = response4.data.cast;
          //console.log('TV cast' + this.TVCast)

          for(this.i=0;this.i<this.movieList.length;this.i++){
            this.movieIDList.push(this.movieList[this.i].id);
          }
          
          
          for(this.i=0;this.i<this.TVList.length;this.i++){
            this.tvIDList.push(this.TVList[this.i].id);
          }

          /*for(this.i=0;this.i<this.cast.length;this.i++){
            this.actorNames.push(this.cast[this.i].name);
          }*/

          /*for(this.i=0;this.i<this.results.length;this.i++) {
            this.ID = this.results[this.i]
            console.log('ID' + this.ID)
          }*/

          for(this.i=0;this.i<this.movieIDList.length;this.i++) {
            this.movieID = this.movieIDList[this.i]
            //console.log(this.movieID)
          } 

          for(this.i=0;this.i<this.tvIDList.length;this.i++) {
            this.tvID = this.tvIDList[this.i]
            //console.log(this.tvID)
          }
          //I can combine the lists like this which will feed into the "results" array in data
          this.results = [...this.movieIDList, ...this.tvIDList]

      }))
      .catch(function (error) {
      // handle error
      console.log(error);
      })
      .then(function() {

   
      });
    },

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
