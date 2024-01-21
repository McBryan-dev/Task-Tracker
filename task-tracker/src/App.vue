<template>

  <div class="container">

    <Header title="Task Tracker" @show-add-tasks= "toggleAddTasks" :showTasks= "showAddTasks"/>

    <div v-if= "showAddTasks">

      <AddTask @add-task= "addTask" />

    </div>

    <Tasks @toggle-rem="toggleRem" @delete-task="deleteTask" :tasks="tasks"/>

  </div>

</template>

<script>

  import Header from './components/Header.vue'
  import Tasks from './components/Tasks.vue'
  import AddTask from './components/AddTask.vue'

  export default {
    name: 'App',
    components: {
      Header,
      Tasks,
      AddTask
    },

    data() {
      return {
        tasks: [],
        showAddTasks: false
      }
    },

    methods: {

      toggleAddTasks() {
        this.showAddTasks = !this.showAddTasks
      },

      addTask(task) {
        this.tasks = [...this.tasks, task]
      },

      deleteTask(id) {

        if(confirm('Are you sure')) {
          this.tasks = this.tasks.filter((task) => task.id !== id)
        }
       
      },

      toggleRem(id) {
        this.tasks = this.tasks.map((task) => 
        task.id === id ? { ...task, reminder: !task.reminder} : task
        )
      },

      async fetchTasks() {

        const res = await fetch('http://localhost:3000/tasks')

        const data = await res.json()

        return data

      },

      async fetchTask(id) {

        const res = await fetch(`http://localhost:3000/tasks/${id}`)

        const data = await res.json()

        return data

      }

    },

    async created() {

      this.tasks = await this.fetchTasks()

    }

  }

</script>

<style>
  * {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
  }

  body {
    font-family: 'Poppins', sans-serif;
  }

  .container {
    margin: 50px auto;
    overflow: auto;
    min-height: 300px;
    border: 1px solid steelblue;
    padding: 30px;
    border-radius: 5px;
  }

  .btn {
    display: block;
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

  .btn-focus {
    outline: none;
  }

  .btn:active {
    transform : scale(0.98);
  }

  .btn-block {
    display: block;
    width: 100;
  }
</style>
