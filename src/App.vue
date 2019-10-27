<template>
  <div id="app">
    <el-container>
      <GanttChart />
      <newGanttChart />
    </el-container>

    <!-- <img src="./assets/logo.png">
    <div>
      <p>
        If Element is successfully added to this project, you'll see an
        <code v-text="'<el-button>'"></code>
        below
      </p>
      <el-button>el-button</el-button>
    </div>
    <HelloWorld msg="Welcome to Your Vue.js App"/> -->
  </div>
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'
import GanttChart from '@/components/echartGanttChart.vue'
import newGanttChart from '@/components/ganttChart.vue'
export default {
  name: 'app',
  components: {
    GanttChart,
    // HelloWorld
    newGanttChart,
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
