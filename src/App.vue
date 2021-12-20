<template> 
  <composition-Api msg="demo!"/> 
  <reactive-Api msg="demo reactive"/> 
  <ref-Api msg="demo ref"/> 
</template> 

<script>
import compositionApi from './view/compositionApi'
import reactiveApi from './view/reactiveApi'
import refApi from './view/refApi'
export default {
  name: 'App',
  components: {
    compositionApi,
    reactiveApi,
    refApi
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
