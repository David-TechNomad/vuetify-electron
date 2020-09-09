<template>
<div class="home-container">
    <el-menu v-if="activeTab!=='-1'" mode="horizontal" :default-active="activeTab" :router="true">
      <el-menu-item
        :index="pathIndex.toString()"
        v-for="(path, pathIndex) in paths"
        :key="pathIndex"
        :route="{path: path.to}"
      >{{path.title}}</el-menu-item>
      <!-- <div class="rt mtmr15">
        <el-button class="defaultBtn" id="minbt" @click="minbt">最小化</el-button> 
        <el-button class="defaultBtn" id="maxbt" @click="maxbt">最大化</el-button>
        <el-button class="defaultBtn" id="closebt" @click="closebt">关闭</el-button> 
      </div> -->
    </el-menu>
    <router-view/>
    <div class="home">
      <h1 style="margin:0 auto; font-size:80px">{{nowTime | dateFormat}}</h1>
      <h2 style="margin:20px auto; font-size: 42px">欢迎来到报表统计平台</h2>
  </div>
  </div>
  
</template>

<style scoped>
.home {
  height: 70vh;
  text-align: center;
  padding-top: 30vh;
}
</style>
<script>
// debugger;
// import electron from 'electron'
// import ElementUI from 'element-ui';
// let ipc = electron.ipcRenderer
// const {ipcRenderer: ipc} = require('electron');
import {ipcRenderer} from 'electron'
  export default {
    data() {
      return {
        activeTab: "0",
        nowTime: Date.now(),
        paths: [
          { to: "/", title: "首页" },
          { to: "/customReportList", title: "拖拽报表 --- 报表列表" },
          // { to: "/editComponent", title: "拖拽报表 --- 编辑组件" },
          // { to: "/palette", title: "仿 Chrome 调色板" },
          // { to: "/waves", title: "水波纹" },
          // { to: "/dragDialog", title: "elementDialog 可拖拽" },
          // { to: "/customLoading", title: "自定义 loading" },
          // { to: "/customScrollbar", title: "自定义 scrollbar" }
          // { to: "/dragList", title: "重新定义拖动" }
      ]
      }
    },
    methods:{
      // maxbt() {
      //   console.log('maxbt')
      //   ipcRenderer.send("window-max")
      // },
      // minbt() {
      //   console.log('minbt')
      //   ipcRenderer.send("window-min")
      // },
      // closebt() {
      //   console.log('closebt')
      //   ipcRenderer.send("window-close")
      // }
  },
    created() {
      setInterval(() => {
        this.nowTime = Date.now()
      }, 1000)
    },
    computed: {
    },
  }
</script>