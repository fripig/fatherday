<template>
  <div id="app">
    <svgEditor :say2father="say2father" v-if="show"></svgEditor>
    <form>
      <div class="form-group">
        <label>打些想對爸爸說的話</label>
        <textarea class="form-control" rows="2" v-model="say2father"></textarea>
      </div>
      <!-- <div class="checkbox">
        <label>
          <input type="checkbox"> 是，確定是全形20個字。多得會被裁掉喔～
        </label>
      </div> -->
      <button class="btn btn-block btn-lg" id="downloadBtn" @click="download">下載</button>
      <button class="btn btn-block btn-lg" id="resetBtn" @click="reset">重新填寫</button>
    </form>
  </div>
</template>

<script>

import svgEditor from './components/svgeditor'
import { bus } from "./bus"

export default {
  name: 'app',
  data() {
    return {
      say2father: "",
      show: true
    }
  },
  mounted() {
    console.log('mounted')
    bus.$on('reset', (id) => {
      this.reset()
    })
  },
  methods: {
    download() {
      bus.$emit('download', 1)
    },
    reset() {
      this.show = false
      this.$nextTick(() => {
        this.show = true
      })
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
}
#downloadBtn{
  background-color: #333333; 
  border-color: #111111;
  color: #eeeeee;
}
#resetBtn{
  background-color: #eeeeee;
  color: #333333;
  border-color: #aaaaaa;
}
</style>
