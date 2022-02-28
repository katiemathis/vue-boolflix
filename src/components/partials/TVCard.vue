<template>
<!-- v-for gets completed on app.vue once all $emits and props are properly identified throughout files-->
<!-- using {{}} here takes each given object from the array and prints it on the screen -->
        <div class="tv-series col">
            <div class="flip-card row justify-content-start">
                <div class="col flip-card-inner">
                    <div class="flip-card-front">
                        <div v-if="TVSeries.poster_path==null">{{TVSeries.name}}</div>
                        <div v-else><img :src= "'http://image.tmdb.org/t/p/w185/' + TVSeries.poster_path" :alt="TVSeries.name"></div>
                    </div>
                    <div class="movie-info flip-card-back">
                        <div class="card-back-info">
                            <div><h6>{{TVSeries.name}}</h6></div>
                            <div class="original-title" :class= "(TVSeries.original_name==TVSeries.name)?'hide':''"><span class="bold">Original Name: </span>{{TVSeries.original_name}}</div>
                            <div v-if= "TVSeries.original_language==''">{{TVSeries.original_language}}</div>
                            <div v-else><lang-flag :iso= "TVSeries.original_language" /></div>
                            <div class="star-ratings">
                                <span :class= "(fiveStarRating==0)?'hide':''"><span class="bold">Avg Rating: </span><i class="fa-solid fa-star" v-for="(rating, index) in fiveStarRating" :key="index"></i></span>
                                <span :class= "(!fiveStarRating==0)?'hide':''"><span class="bold">Be the first to rate: </span><i class="fa-regular fa-star"></i></span>
                            </div>
                            <div class="overview"><span class="bold" :class= "(TVSeries.overview=='')?'hide':''">Overview: </span>{{TVSeries.overview}}</div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
</template>

<script>
import LangFlag from 'vue-lang-code-flags';

export default {
    name: 'TVCard',
    components: {
        LangFlag,
    },
    props: {
        'TVList': Array,
        'TVSeries': Object,
    },
    data () {
        return {
            fiveStarRating: (Math.ceil(this.TVSeries.vote_average))/2
        }
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

            .card-back-info {
                position: relative;
                height: 260px;
                overflow: scroll;

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