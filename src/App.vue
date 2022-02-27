<template>
  <div id="app">
    <MyHeader />  
    <MyMain />
  </div>
</template>

<script>

import MyHeader from './components/MyHeader.vue'
import MyMain from './components/MyMain.vue'


export default {
  name: 'App',
  components: {
    MyHeader,
    MyMain,
 
  }
}
</script>

<style scoped lang="scss">

@import './style/general.scss';

/*#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}*/
</style>
