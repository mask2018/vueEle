<template>
  <div class="head" v-if="hdstate">
    <a href="javascript:;" class="logo">logo</a>
    <div class="search"></div>
    <div class="headClose">
      <router-link to="/components/login/Login">登录</router-link>
      <span class="tool-icon min" @click="headMin()">最小化</span>
      <span class="tool-icon max" @click="headMax()">放大</span>
      <span class="tool-icon close" @click="headClose()">关闭</span>
    </div>
  </div>
</template>

<script>
export default {
  name: 'dacHead',
  data () {
    return {
      isBig: true
    }
  },
  props: {
    hdstate: ''
  },
  methods: {
    headMin: function () {
      var ipcRenderer = require('electron').ipcRenderer
      console.log(1)
      ipcRenderer.send('hide-window')
    },
    headMax: function () {
      var ipcRenderer = require('electron').ipcRenderer
      var isBig
      console.log(2)
      if (isBig) {
        ipcRenderer.send('show-window')
      } else {
        ipcRenderer.send('orignal-window')
      }
      isBig = !isBig
    },
    headClose: function () {
      var ipcRenderer = require('electron').ipcRenderer
      console.log(3)
      ipcRenderer.send('window-all-closed')
    }
  }
}
</script>

<style lang="less" scoped>
.head{
  position: fixed; left: 0; top: 0; width: 100%;
  height: 80px; background-color: chocolate; z-index: 111;
  -webkit-app-region: drag;
  .logo{
    position: absolute; left: 20px; top: 0; -webkit-app-region: no-drag;
  }
  .search{
    text-align: center; -webkit-app-region: no-drag;
  }
  .headClose{
    position: absolute; right: 20px; top: 0;
    text-align: right;
    span{
      display: inline-block; margin-left: 20px; cursor: pointer; color: #fff;
      -webkit-app-region: no-drag;
    }
    a{ -webkit-app-region: no-drag;}
  }
}
</style>
