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
      
      <Task name="example"/>
      
      <Task name="example"/>

    <div>
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
      /*var config = {
        method: 'post',
        url: 'http://localhost:8000/task'
      }*/
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
        let obj = {
        name: this.task.name,
        description: this.task.description
        }
        axios.post("http://localhost:3000/task", obj).then(() =>{
          console.log(obj);
        })
        .catch(function (error) {
          console.log(error);
        });
        

        /*var data = JSON.stringify({
          name: "",
          description: ""
        });

        var config = {
          method: 'post',
          url: 'http://localhost:3000/task',
          headers: { 
            'Content-Type': 'application/json'
          },
          data : data
        };

        axios(config)
        .then(function (response) {
          console.log(JSON.stringify(response.data));
        })
        .catch(function (error) {
          console.log(error);
        });*/
        
        /*axios({
          method: 'post',
          url: 'http://localhost:3000/task',
          data: {
            name: 'Fred',
            description: 'Flintstone'
          }
        });*/

        /*axios.post('http://localhost:3000/task', {
          name: 'Fred',
          description: 'Flintstone'
        })
        .then(function (response) {
          console.log(response);
        })
        .catch(function (error) {
          console.log(error);
        });*/
        
        /*axios({
        method: 'post',
        url: 'http://localhost:3000/task',
        data: {
          name: "teste",
          description: "mais teste"
        }
        }).then(res =>{
          let results = res.data;
          var response = res.data;
          
          console.log("ENTROU");
          console.log(results);
          console.log(response);
          console.log(res);
        }).catch(error => {
        console.log(error);
        });*/
        /*axios.post(`/task/`).then(res => 
        {
          console.log("ENTROU");
          console.log(this.task);
          console.log(res);
          //this.tasks = res.data.results;
        })*/
        /*axios(config).then(function (res) 
        {
          console.log("ENTROU");
          console.log(this.task);
          console.log(res);
          //this.tasks = res.data.results;
        })*/
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
