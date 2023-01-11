<template>
  <div class="container">
    <Header
      @toggle-add-task="toggleAddTask"
      title="Task Tracker"
      :showAddTask="showAddTask"
    />
    <AddTask v-show="showAddTask" @add-task="addTask" />
  <Tasks
    @toggle-reminder="toggleReminder"
    @delete-task="deleteTask"
    :tasks="tasks"
  />
    <Footer />
  </div>
</template>

<script>
import Header from './components/Header'
import Footer from './components/Footer'
import Tasks from './components/Tasks'
import AddTask from './components/AddTask'

export default {
  name: 'App',
  components: {
    Header,
    Footer,
    Tasks,
    AddTask,
  },
  data() {
    return {
      showAddTask: false,
      tasks: [
        {
          id: 1,
          text: 'Go to Doctor',
          day: 'March 1st at 11:30am',
          reminder: true
        },
        {
          id: 2,
          text: 'Shopping',
          day: 'March 8th at 2:00pm',
          reminder: true
        },
        {
          id: 3,
          text: 'School Meeting',
          day: 'March 16th at 5:30pm',
          reminder: false
        }
      ],
    }
  },
  methods: {
    toggleAddTask() {
      this.showAddTask = !this.showAddTask
    },
    addTask(task) {
      const newTask = {
        id: Math.ceil(Math.random() * 10000),
        text: task.text,
        day: task.day,
        reminder: task.reminder
      }
      this.tasks.push(newTask)
    },
    deleteTask(id) {
      this.tasks = this.tasks.filter(item=> item.id !== id)
    },
    toggleReminder(id) {
      this.tasks = this.tasks.map(item => item.id === id ? 
      {...item, reminder: !item.reminder} : item)
    },
    fetchTasks() {
      console.log("fetchTasks")
    },
    fetchTask(id) {
      console.log("fetchTask")
    },
    created() {
      console.log("created")
    },
  },
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
  overflow: auto;
  min-height: 300px;
  border: 1px solid steelblue;
  padding: 30px;
  border-radius: 5px;
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
</style>