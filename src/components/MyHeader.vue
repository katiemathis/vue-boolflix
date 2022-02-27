<template>
    <div class="container">
        <div class="row">
            <!-- logo -->
            <div class="col">
                <h1>BOOLFLIX</h1>
            </div>

            <!-- search bar where user inputs partial or full movie title -->
            <!-- on click, user sees all movies which contain search input -->
            <div class="col">
                <input type="text" v-model= "movieSearchText">
                <button>SEARCH</button>
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
    }
}
</script>

<style lang="scss" scoped>

@import '../style/general.scss';

</style>