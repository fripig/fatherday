<template>
  <div id="app">
    <input type="text" v-model="fathername">
    <svgEditor :fathername="fathername"></svgEditor>
  </div>
</template>

<script>

import svgEditor  from './components/svgeditor'

export default {
  name: 'app',
  data(){
    return {
      fathername : ""
    }
  },
  components: {
    svgEditor
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
