<template>
        <div class="movies col">
            <div class="flip-card row justify-content-start">
                <div class="col flip-card-inner">
                    <div class="flip-card-front">
                        <div v-if="movie.poster_path==null">{{movie.title}}</div>
                        <div v-else><img :src= "'http://image.tmdb.org/t/p/w185/' + movie.poster_path" :alt="movie.title"></div>
                    </div>
                    <div class="movie-info flip-card-back">
                        <div><h6>{{movie.title}}</h6></div>
                        <div class="original-title" :class= "(movie.original_title==movie.title)?'hide':''"><span class="bold">Original Title: </span>{{movie.original_title}}</div>
                        <div v-if= "movie.original_language==''">{{movie.original_language}}</div>
                        <div v-else><lang-flag :iso= "movie.original_language" /></div>
                        <div class="star-ratings">
                            <span :class= "(fiveStarRating==0)?'hide':''"><span class="bold">Avg Rating: </span><i class="fa-solid fa-star" v-for="(rating, index) in fiveStarRating" :key="index"></i></span>
                            <span :class= "(!fiveStarRating==0)?'hide':''"><span class="bold">Be the first to rate: </span><i class="fa-regular fa-star"></i></span>
                        </div>
                        <div class="overview"><span class="bold" :class= "(movie.overview=='')?'hide':''">Overview: </span>{{movie.overview}}</div>
                    </div>
                </div>
            </div>
        </div>
</template>

<script>
import LangFlag from 'vue-lang-code-flags';
export default {
    name: 'MovieCard',
    components: {
        LangFlag,
    },
    props: {
        'movieList': Array,
        'movie': Object,
    }, 
    data () {
        return {
            fiveStarRating: (Math.ceil(this.movie.vote_average))/2
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
                overflow-y: scroll;
            }
        }
    }

    

}


</style>