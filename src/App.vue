<template> 
  <composition-Api msg="demo!"/> 
  <reactive-Api msg="demo reactive"/> 
  <ref-Api msg="demo ref"/> 
  <readonly-Api msg="readonlu ref"/> 
</template> 

<script>
import compositionApi from './view/compositionApi'
import reactiveApi from './view/reactiveApi'
import refApi from './view/refApi'
import readonlyApi from './view/readonlyApi'
export default {
  name: 'App',
  components: {
    compositionApi,
    reactiveApi,
    refApi,
    readonlyApi
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
