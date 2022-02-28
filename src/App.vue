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
      rating: [],
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
        axios.get('https://api.themoviedb.org/3/search/tv', params)
      ])
        //by differentiating the different responses, I'm able to keep both lists separate
      .then(axios.spread((response1, response2) => {
          this.movieList = response1.data.results;
          this.TVList = response2.data.results;
        //this allows me to parse out the ratings for each of the elements so I can later
        //use them in a v-for, convert to a 5-point scale and use a star icon for each point
          this.movieList.forEach(movie => {
            let fiveStar = (Math.floor(movie.vote_average))/2;

            this.rating.push(fiveStar);
            console.log('movie'+this.rating)
          });
          this.TVList.forEach(TVSeries => {
            let fiveStar = (Math.floor(TVSeries.vote_average))/2;

            this.rating.push(fiveStar);
            console.log('TV'+this.rating)
          }
          )
      }))
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
