<template>
  <div id="app">
      <MyHeader @textEnteredEvt="retrieveTextEntered"/>
      <MyMain 
      :movieList="movieList" :movie="movie"    
      v-for= "(movie, index) in filteredList" :key= "index"
      />
      <!-- v-for on MyMain cycles through the array and provides the data from each individual movie -->
  </div>
</template>

<script>
const axios = require('axios');

import MyHeader from './components/MyHeader.vue'
import MyMain from './components/MyMain.vue'


export default {
  name: 'App',
  components: {
    MyHeader,
    MyMain,
 
  },
  data() {
    return {
      textEntered: '',
      movie: {},
      movieList: [],
      filteredMovies: [],
    }
  },
  computed:{
    filteredList() {
      if(this.textEntered == '') {
        return this.movieList;
      }else{
        return this.filteredMovies; 
        }
      }
    },
  methods: {
    retrieveTextEntered(textEnteredEvt) {
      this.textEntered = textEnteredEvt;
      console.log(this.textEntered)

      this.movieList.forEach((movie) => {
        if(movie.title.toLowerCase().includes(this.textEntered.toLowerCase())) {
          this.filteredMovies.push(movie)
          console.log(movie)
        }
      });
    },
    getMovies() {
                // Make a request for a user with a given ID
                axios.get('https://api.themoviedb.org/3/search/movie?api_key=96259ec6f4490ebbbfaa7d8faba469f1&language=en-US&query=joker&page=1&include_adult=false')
                .then((response) => {
                    this.movieList = response.data.results;
                    //this.loadingInProgress = false;
                    
                })
                .catch(function (error) {
                    // handle error
                    console.log(error);
                });
            }
        },
        /*mounted() {
            document.onreadystatechanges = () => {
                if (document.readyState == "complete") {
                    this.isloaded = true;
                }
            }
        },*/
        created() {
            this.getMovies();
            //this.loadingInProgress = false;
            
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
