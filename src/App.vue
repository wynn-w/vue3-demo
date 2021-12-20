<template> 
  <composition-Api msg="demo!"/> 
</template> 

<script>
import compositionApi from './view/compositionApi'
export default {
  name: 'App',
  components: {
    compositionApi
  }

}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
