<template>
  <div id="app">
    <div class="my-5">
      <h3>Todoister</h3>
    </div>
      
      <div class="d-flex flex-column justify-content-center align-items-center h-100 my-3">
        <div class="inputParam d-flex flex-column justify-content-center align-items-center my-2">
          <b-form-input        
            type="text"
            placeholder="To do task"
            v-model="task.name"
            :state="isValid.name"
          >
          </b-form-input>
            <b-form-invalid-feedback :state="isValid.name">
              Your task needs a name!
            </b-form-invalid-feedback>
        </div>
      </div>

      <div class="d-flex flex-column justify-content-center align-items-center h-100 my-2">
        <div class="inputParam d-flex flex-column justify-content-center align-items-center my-1">
          <b-form-textarea
            type="text"
            placeholder="To do task description"
            rows="3"
            v-model="task.description"
            :state="isValid.description"
          >
          </b-form-textarea>
            <b-form-invalid-feedback :state="isValid.description">
              Your task needs a description!
            </b-form-invalid-feedback>
        </div>
      </div>
    <div>
        <b-button @click.prevent="addTask()">Add task!</b-button>
    </div>

    <div class="column is-half is-offset-one-quarter">
      <div v-for="(item,index) in tasks" :key="index">
        <Task :name="item.name" :description="item.description" :status="item.status"/>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import Task from './components/Task.vue'
export default {
  name: 'App',
  data(){
    return{
      isValid: {
        name: null,
        description: null
      },
      task: {
        name: "",
        description: ""        
      },
      tasks: []
    }
  },
  components: {
    Task
  },
  methods: {
    addTask(){
      axios.get(`${this.API_ENDPOINT}/task/`).then(res => 
      {
        this.tasks = res.data.results;
      })
      //checks if input task.name is valid
      if(this.task.name.length > 1){
        this.isValid.name = true;
      } else {
        this.isValid.name = false;
      }
      //checks if input task.description is valid
      if(this.task.description.length > 1){
        this.isValid.description = true;
      } else {
        this.isValid.description = false;
      }

      if(this.validation){
        console.log("Valid");
      }
    }
  },
  computed:{
    validation(){
      if(this.isValid.name == true && this.isValid.description == true){
        return true;
      } else {
        return false;
      }
    }
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
.inputParam{
  min-width: 400px;
  width: 35%;
}
</style>
