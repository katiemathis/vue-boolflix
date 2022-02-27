<template>
    <div class="main">
        <div class="container">
            <div class="row">
                <!-- logo -->
                <div class="col-7">
                    <h1>BOOLFLIX</h1>
                </div>

                <!-- search bar where user inputs partial or full movie title -->
                <!-- on click, user sees all movies which contain search input -->
                <div class="col-5">
                    <input type="text" placeholder="Enter title of movie..." v-model= "movieSearchText" v-on:keyup.enter="$emit('textEnteredEvt', movieSearchText)">
                    <!-- by using the $emit function, the details in this component get sent to the "padre" app -->
                    <button @click="$emit('textEnteredEvt', movieSearchText)">SEARCH</button>
                </div>
            </div>
        </div>
    </div>
  
</template>

<script>
export default {
    name: 'MyHeader',
    data () {
        return {
            movieSearchText: '',
        }
    },
    /*methods: {
        searchEntered() {
            alert(this.movieSearchText)
            this.textEntered = this.movieSearchText
        }
    }*/


    

}
</script>

<style lang="scss" scoped>

@import '../style/general.scss';

.main {
    background-color: $colorHeader;
    width: 100%;
    height: 70px;

    .container {
        width: 90%;
        margin: auto;

        
        .col-7 {
            align-self: center;

            h1 {                    
                color: $colorNetflixRed;
                line-height: 70px;
            }
        }
        .col-5 {
            align-self: center;
        }

    }
}

</style>