<template>
            <div class="flip-card row justify-content-start" >
                <div class="col flip-card-inner">
                    <div class="flip-card-front">
                        <div v-if="info.poster_path">
                            <img :src= "'http://image.tmdb.org/t/p/w185/' + info.poster_path" :alt="getTitle()">
                        </div>
                        <div v-else class="no-poster">
                            <h2>{{getTitle()}}</h2>
                            <i class="fas fa-film"></i>
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
export default {
    name: 'MyCard',
    components: {
        LangFlag,
    },
    props: {
        'TVList': Array,
        'movieList': Array,
        'info': Object,
        'tvID': Number,
        'tvIDList': Array,
        //'actorsNames': Array
    }, 
    computed: {
        getComputedStar() {
            return Math.ceil(this.info.vote_average /2);
        }
    },
    methods: {
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
        getCastProva() {
            console.log('the get cast prova worked')
        }
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
    height: 278px;
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
                height: 260px;
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