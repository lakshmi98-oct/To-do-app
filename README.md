<!DOCTYPE html>
<html>
<head>
  <title>Vue To-Do App</title>

  <!-- Vue CDN -->
  <script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>

  <style>
    body{
      font-family: Arial;
      background:#f4f4f4;
      display:flex;
      justify-content:center;
      margin-top:50px;
    }

    .container{
      background:white;
      padding:20px;
      width:350px;
      border-radius:10px;
      box-shadow:0 0 10px rgba(0,0,0,0.1);
    }

    h2{
      text-align:center;
    }

    input{
      width:70%;
      padding:10px;
    }

    button{
      padding:10px;
      cursor:pointer;
    }

    ul{
      list-style:none;
      padding:0;
    }

    li{
      display:flex;
      justify-content:space-between;
      background:#eee;
      margin-top:10px;
      padding:10px;
      border-radius:5px;
    }

    .completed{
      text-decoration: line-through;
      color: gray;
    }
  </style>
</head>

<body>

<div id="app" class="container">

  <h2>To-Do App</h2>

  <input 
    type="text" 
    v-model="newTask" 
    placeholder="Enter task"
    @keyup.enter="addTask"
  >

  <button @click="addTask">Add</button>

  <ul>
    <li v-for="(task,index) in tasks" :key="index">

      <span 
        :class="{completed: task.done}"
        @click="task.done = !task.done"
      >
        {{ task.text }}
      </span>

      <button @click="removeTask(index)">❌</button>

    </li>
  </ul>

</div>

<script>
const { createApp } = Vue;

createApp({
  data() {
    return {
      newTask: '',
      tasks: []
    }
  },

  methods: {

    addTask() {

      if(this.newTask.trim() !== ''){

        this.tasks.push({
          text: this.newTask,
          done: false
        });

        this.newTask = '';
      }
    },

    removeTask(index) {
      this.tasks.splice(index,1);
    }

  }
}).mount('#app');
</script>

</body>
</html>
