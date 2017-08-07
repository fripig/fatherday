<template>
  <div id="app">
    讓臉書創辦⼈⾺克祖克伯住每位⽗親⽗親節快樂！
    輸⼊你想祝福的⽗親名字：<input type="text" v-model="fathername">
    <svgEditor :fathername="fathername"></svgEditor>
    <button @click="download">download</button>
  </div>
</template>

<script>

import svgEditor  from './components/svgeditor'
import {bus} from "./bus"

export default {
  name: 'app',
  data(){
    return {
      fathername : ""
    }
  },
  methods:{
    download(){
      bus.$emit('download', 1)
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
