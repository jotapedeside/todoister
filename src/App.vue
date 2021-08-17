<template>
  <div id="app">    
    <div class="column is-half is-offset-one-quarter">
      <div v-for="(task,index) in tasks" :key="index">
        <Task :name="task.name" :description="task.description" :num="index+1" :status="false"/>
      </div>
    </div>
  </div>
</template>

<script>
import Task from './components/Task.vue'
export default {
  name: 'App',
  data(){
    return{
      tasks: []
    }
  },
  components: {
    Task
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
