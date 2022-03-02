<template>
            <div class="flip-card row justify-content-start" >
                <div class="col flip-card-inner">
                    <div class="flip-card-front">
                        <div v-if="info.poster_path!=null">
                            <img :src= "'http://image.tmdb.org/t/p/w185/' + info.poster_path" :alt="getTitle()">
                        </div>
                        <div v-else class="no-poster">
                            <h2>{{getTitle()}}</h2>
                            <i class="fas fa-film"></i>
                        </div> 
                        <div class="front-card-details">
                            <h6>{{getTitle()}}</h6>
                            <div class="star-ratings">
                                <div :class= "(getStar()==0)?'hide':''">
                                    <i class="fa-star" :class= "(i <= getStar())?'fa-solid':'fa-regular'" 
                                    v-for="i in 5" :key="i"></i>
                                </div>
                                <div :class= "(!getStar()==0)?'hide':''">
                                    <i class="fa-regular fa-star"></i>
                                </div>
                            </div>
                        </div>                       
                    </div>
                    <div class="movie-info flip-card-back">
                        <div class="card-back-info">
                            <div><h6>{{getTitle()}}</h6></div>
                            <h6>{{info.ID}}</h6>
                            <div class="original-title" :class= "(getOriginalTitle()==getTitle())?'hide':''">
                                <span class="bold">Original Title: </span>
                                {{getOriginalTitle()}}
                            </div>
                            <div class="original-lang" :class= "(!info.original_language==null)?'hide':''">
                                <lang-flag :iso= "info.original_language" />
                            </div>
                            <div class="star-ratings">
                                <div :class= "(getStar()==0)?'hide':''">
                                    <span class="bold">Avg Rating: </span>
                                    <i class="fa-star" :class= "(i <= getStar())?'fa-solid':'fa-regular'" 
                                    v-for="i in 5" :key="i"></i>
                                </div>
                                <div :class= "(!getStar()==0)?'hide':''">
                                    <span  class="bold">Be the first to rate: </span>
                                    <i class="fa-regular fa-star"></i>
                                </div>
                            </div>
                            <div class="overview">
                                <span class="bold" :class= "(info.overview=='')?'hide':''">Overview: </span>
                                {{info.overview}}
                            </div>
                            <ul class="actors" >
                                <span class="bold">Starring: </span>
                                <p>{{actor}}</p>
                            </ul>
                            <div class="genre-ids">
                                <span class="bold" :class= "(info.overview=='')?'hide':''">Genres: </span>
                                {{info.genre_ids}}
                            </div>
                                
                        </div>
                    </div>
                </div>
            </div>
</template>

<script>
import LangFlag from 'vue-lang-code-flags';
const axios = require('axios');

export default {
    name: 'MyCard',
    components: {
        LangFlag,
    },
    data() {
        return {
            castList: [],
            actorsNames: [],
            api_key: '96259ec6f4490ebbbfaa7d8faba469f1',
            language: 'en-US',
            actor: '',
            movieID: '',
            eachMovieCastList: [],
        }
    },
    props: {
        'TVList': Array,
        'movieList': Array,
        'info': Object,
        'tvID': Number,
        'tvIDList': Array,
        'movieIDList': Array,
        //'actorsNames': Array,
        //'actor': String,
        //'castList': Array,
        //'movieID': Number,
        //'api_key': String,
        //'language': String,
    }, 
    mounted() {
        this.getMovieID();
        this.getCast(); 
       
    },
    computed: {
        getComputedStar() {
            return Math.ceil(this.info.vote_average /2);
        },
    },
    methods: {
        getMovieID() {
            this.movieID.forEach(movieID => {
                movieID = this.movieID
                return movieID
            })
          /*for(this.i=0;this.i<this.movieIDList.length;this.i++) {
            this.movieID = this.movieIDList[this.i]
            console.log(this.movieID)
          }*/
        }, 
        getTitle() {
            if (this.info.title) {
                return this.info.title;
            } else {
                return this.info.name;
            }
        },
        getOriginalTitle() {
            if (this.info.original_title) {
                return this.info.original_title;
            } else {
                return this.info.original_name;
            }
        },
        getStar() {
            return Math.ceil(this.info.vote_average /2);
        }, 
        getCast() {
                // Make a request for a user with a given ID
            this.movieIDList.forEach(movieID => {
                //this axios call is using the movieID to generate a list of credits data 
                axios.get('https://api.themoviedb.org/3/movie/'+ movieID + '/credits?api_key='+ this.api_key + '&language=' + this.language)
                .then((response) => {
                    //credits go here and by adding .cast, I extrapolate only the cast list info
                    this.castList = response.data.cast;
                    console.log(this.castList)

                    //I cycle the cast list to get the first five actors' names
                    for(this.i=0;this.i<5;this.i++){
                    this.actorsNames.push(this.castList[this.i].name);
                    console.log(this.actorsNames)
                    }

                    //I cycle the first five actors' names to get each individual name (maybe a forEach would go better here?) 
                    this.actorsNames.forEach(actor => {
                        console.log('this is each actors name in mycard' + actor)
                    })

                    
                
                    

                    //this.getCastNames();

                })
                .catch(function (error) {
                    // handle error
                    console.log(error);
                })
                .then(function () {

                });
                this.eachMovieCastList.push(this.actorsNames)
            })
        },
    
    }




            
        
}
</script>

<style lang="scss">

@import '../../style/general.scss';

*{
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

.show {
    display: block;
}

.hide {
    display: none;
}

.bold {
    font-weight: 600;
}

.flip-card {
    background-color: transparent;
    padding: 0;
    width: 185px;
    height: 400px;
    perspective: 1000px;
    &:hover .flip-card-inner {
        transform: rotateY(-180deg);
        cursor: pointer;
    }

    .flip-card-inner {
        position: relative;
        width: 100%;
        height: 100%;
        text-align: center;
        transition: transform 0.8s;
        transform-style: preserve-3d;
        

        .flip-card-front {
            position: absolute;
            padding: 0;
            margin: 0;
            width: 100%;
            height: 100%;
            -webkit-backface-visibility: hidden; /* Safari */
            backface-visibility: hidden;
            background-color: $colorHeader;
            color: #fff;

            .front-card-details {
                padding: 10px;

            }

            .no-poster {
                color: #fff;
                text-transform: uppercase;
                align-self: center;
                padding: 20px;
                background-color: rgba(219, 0, 18, 0.2);
                height: 100%;

                .fa-film {
                    font-size: 6em;
                    margin-top: 10px;
                }
            }
        }
        .flip-card-back {
            position: absolute;
            padding: 10px;
            margin: 0;
            width: 100%;
            height: 100%;
            -webkit-backface-visibility: hidden; /* Safari */
            backface-visibility: hidden;
            background-color: $colorHeader;
            color: #fff;
            transform: rotateY(180deg);
            text-align: left;

            .card-back-info {
                position: relative;
                height: 380px;
                overflow-y: scroll;
            
                .star-ratings {
                    color: #fff;
                    font-size: small;
                    .fa-star {
                        color: gold;
                    }
                    .fa-regular {
                        color: #fff;
                    }

                }
                .original-title {
                    font-style: italic;
                    font-size: small;
                }
                .overview {
                    font-size: small;
                    
                }
            }
        }
    }

    

}


</style>