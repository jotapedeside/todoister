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
    <div>      
        <b-button class="inputParam my-3" @click.prevent="pressedChecker()">{{taskVisualizer}}</b-button>
    </div>
    <div>
      <div v-for="(item,index) in tasks" :key="index">
        <Task :id="item._id" :name="item.name" :description="item.description" :status="item.status" @deleteMe="deleteTask($event)" @completeMe="completeTask($event)"/>
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
      taskVisualizer: "",
      pressed: null,
      pages: 1,
      currentPage: 1,
      pageLimit: 10,
      total: 0,
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
      //axios POST method to add tasks
      if(this.validation){
        let obj = {
        name: this.task.name,
        description: this.task.description
        }
        axios.post("http://localhost:3000/task", obj).then(() =>{
          console.log(obj);
          this.listTasks(this.currentPage, 10, "asc");
        })
        .catch(function (error) {
          console.log(error);
        });
      }
    },
    //axios GET method to list tasks
    listTasks(page, pageLimit, sort){
      axios.get(`http://localhost:3000/task/${page}/${pageLimit}/${sort}`).then(res =>{
        this.tasks = res.data.data;
        this.pages = Math.ceil(Math.max(1, res.data.count/10));
        this.currentPage = page;
        this.pageLimit = pageLimit;
        this.total = res.data.count;
      }).catch(error => {
      console.log(error);
      })
    },
    //axios GET method to list tasks done
    listDoneTasks(page, pageLimit, sort){
      axios.get(`http://localhost:3000/done/${page}/${pageLimit}/${sort}`).then(res =>{
        this.tasks = res.data.data;
        this.pages = Math.ceil(Math.max(1, res.data.count/10));
        this.currentPage = page;
        this.pageLimit = pageLimit;
        this.total = res.data.count;
      }).catch(error => {
      console.log(error);
      })
    },
    //axios PATCH method to change task status
    completeTask: function($event){
      var id = $event.taskId;
      axios.patch(`http://localhost:3000/task/${id}`).then(res =>{
          this.pageValidation();
          console.log(res);
      })
      console.log(id);
    },
    //axios DELETE method to delete tasks
    deleteTask: function($event){
      var id = $event.taskId;
      axios.delete(`http://localhost:3000/task/${id}`).then(res =>{
          this.pageValidation();
          console.log(res);
      })
      .catch(function (error) {
        console.log(error);
      });
    },
    pageValidation(){
      if(this.pressed == false){
        this.taskVisualizer = "Tasks Done";
        return this.listTasks(1, 10, 'asc');
      } else {
        this.taskVisualizer = "Tasks Not Done";
        return this.listDoneTasks(1, 10, 'asc');
      }
    },
    pressedChecker(){      
        this.pressed = !this.pressed;
        this.pageValidation();
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
  },
  created(){
    this.listTasks(1, 10, "asc");
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
