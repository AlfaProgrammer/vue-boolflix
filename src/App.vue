<template>
  <div id="app">
    <BoolMain />
  </div>
</template>

<script>
import BoolMain from "./components/BoolMain.vue"
export default {
  name: 'App',
  components: {
    BoolMain
  }
}
</script>

<style lang="scss">
@import '~@fortawesome/fontawesome-free/css/all.css';
*{
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  } 

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;

}
</style>
