<template>
  <Header title="Task Reminder" />
  <div class="container">
    <Tasks
      @toggle-reminder="toggleReminder"
      @add-task="addTask"
      @delete-task="deleteTask"
      :tasks="tasks"
      :taskId="taskId"
    />
  </div>
  <input type="hidden" :value="setToLocalStorage" />
  <!-- Set to localstorage  -->
  <footer style="position: absolute; bottom: 0px; text-align: center; display: block; margin: 3px auto;">
    Copyright&copy; Made By Fahad
  </footer>
</template>

<script>
import Header from "./components/Header.vue";
import Tasks from "./components/Tasks.vue";

export default {
  name: "App",
  components: {
    Header,
    Tasks,
  },
  data() {
    return {
      tasks: [],
      tasksArr: JSON.parse(localStorage.getItem("tasks")),
      taskId: 1
    };
  },

  methods: {
    addTask(taskObj) {
      this.tasks = [...this.tasks, taskObj];
      this.taskId+=1
      console.log(this.tasks);
    },
    deleteTask(id) {
      this.tasks = this.tasks.filter((task) => task.id !== id);
      console.log("task", this.tasks);
    },
    toggleReminder(id) {
      this.tasks = this.tasks.map((task) =>
        task.id === id ? { ...task, reminder: !task.reminder } : task
      );
      console.log("task", this.tasks);
    },
  },
  computed: {
    setToLocalStorage: function () {
      localStorage.setItem("tasks", JSON.stringify(this.tasks));
      return "Setted";
    },
  },
  created() {
    this.tasks = this.tasksArr || this.tasksArr == [] ? this.tasksArr : [];
    this.taskId = this.tasks.length>0? (this.tasks[this.tasks.length - 1].id)+1: 1
  },
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
#app {
  font-family: cursive, Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 30px;
  box-sizing: border-box;
}
.container {
  width: 85%;
  margin: auto;
}
</style>
