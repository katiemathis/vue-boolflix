<template>
    <div class="d-flex justify-content-center align-items-center welcome">
        <h1>Search movie or TV title</h1>
 
        <div class="d-flex justify-content-center align-items-center page_loader" >
        <div class="cube"></div>
        <div class="cube"></div>
        <div class="cube"></div>
        <div class="cube"></div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'PageLoading',
    loadingInProgress: true,

}
</script>

<style scoped lang="scss">

@import '../style/general.scss';

* {
    width: 100vw;
    background-color: $colorBackground;
}

.welcome {
    position: fixed;
    top: 70px;
    left: 0;
    right: 0;
    bottom: 0;
    color: $colorNetflixRed;
    h1 {
        text-align: center;
        text-transform: uppercase;
    }
}



.page_loader {
    position: fixed;
    top: 200px;
    left: 0;
    right: 0;


    .cube {
        width: 40px;
        height: 40px;
        margin-right: 10px;
        border-radius: 50%;
        
        @for $i from 1 through length($colors) {
            &:nth-child(#{$i}) {
                background-color: nth($colors, $i);
                border: solid 1px #000;
            }
        }

        &:first-child {
            animation: left 3s infinite;
        }
        &:last-child {
            animation: right 3s infinite 1.5s;
        }
    }
}
@keyframes left {
    40% {
        transform: translatex(-60px);
    }
    50% {
        transform:translatex(0);
    }
}
@keyframes right {
    40% {
        transform: translatex(60px);
    }
    50% {
        transform:translatex(0);
    }
}
</style>