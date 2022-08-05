<template>
  <div class="container">

    <Header @btn-click="toggleAddTask" :showAddTask="showAddTask" :name="'Task Tracker'" />
    <AddTask v-if="showAddTask" v-on:add-task="addTask" />
    <Tasks v-if="!isLoading" v-bind:tasks="tasks" @delete-task="deleteTask" @toggle-reminder="toggleReminder" />
    <div class="d-grid" v-else>
      <Spinner />
    </div>
  </div>
</template>

<script>
import Header from './components/Header.vue'
import AddTask from './components/AddTask.vue'
import Tasks from './components/Tasks.vue'
import axios from 'axios';
import { URLS } from './utils/constants'
import Spinner from './components/Spinner.vue';

export default {
  name: 'App',
  components: {
    Header,
    AddTask,
    Tasks,
    Spinner
},
  data() {
    return {
      isLoading: false,
      tasks: [],
      showAddTask: true,
    }
  },
  methods: {
    async addTask(task){
      const res = await axios.post(URLS.TASKS, task, { headers: {
        'Content-type': 'application/json'
      } })
      this.tasks = [...this.tasks, res.data];
    },
    async deleteTask(id){
      if(!confirm("Are you sure to delete the task?")) return;
      const res = await axios.delete(`${URLS.TASKS}/${id}`);
      if(res.status === 200){
        this.tasks = this.tasks.filter(task => task.id !== id);
      }
      
    },
    toggleAddTask(){
      this.showAddTask = !this.showAddTask
    },
    async toggleReminder(id){
      const index = this.tasks.findIndex(task => id === task.id); 
      const updatedTask = {
        ...this.tasks[index],
        reminder: !this.tasks[index].reminder
      }
      const res = await axios.put(`${URLS.TASKS}/${id}`, updatedTask, { headers: { 'Content-type': 'application/json' } })
      if(res.status === 200){
        this.tasks = this.tasks.map(task => {
          if (task.id === id) {
            return updatedTask
          }
          return task;
        })
      }
    }
  },
  created() {
    (async()=> {
      this.isLoading = true;
      const res = await axios.get(URLS.TASKS);
      this.isLoading = false;
      if(res.status === 200){
        this.tasks = res.data
        return;
      }
      this.tasks = []
    })()
  }
  
}
</script>

<style>
    @import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;400&display=swap');
  
    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
    }
  
    body {
      font-family: 'Poppins', sans-serif;
    }
  
    .container {
      max-width: 500px;
      margin: 30px auto;
      height: calc(100vh - 60px);
      border: 1px solid steelblue;
      padding: 30px;
      border-radius: 5px;
      overflow-y: auto;
      box-sizing: border-box;
    }
  
    .btn {
      display: inline-block;
      background: #000;
      color: #fff;
      border: none;
      padding: 10px 20px;
      margin: 5px;
      border-radius: 5px;
      cursor: pointer;
      text-decoration: none;
      font-size: 15px;
      font-family: inherit;
    }
  
    .btn:focus {
      outline: none;
    }
  
    .btn:active {
      transform: scale(0.98);
    }
  
    .btn-block {
      display: block;
      width: 100%;
    }

    .d-grid{
      display: grid;
      place-items: center;
    }

</style>
