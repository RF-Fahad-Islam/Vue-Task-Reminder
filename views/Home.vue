<template>
  <div class="home">
    <Header title="Task Reminder" />
    <div class="container">
      <Tasks
        @toggle-reminder="toggleReminder"
        @add-task="addTask"
        @delete-task="deleteTask"
        @delete-all="deleteAll"
        :tasks="tasks"
        :taskId="taskId"
      />
    </div>
    <input type="hidden" :value="setToLocalStorage" />
    <!-- Set to localstorage  -->
    <footer
      style="
        position: relative;
        bottom: 0px;
        text-align: center;
        display: block;
        margin: 10px auto;
      "
    >
      Copyright&copy; Made By Fahad
    </footer>
  </div>
</template>


<script>
import Header from "../components/Header.vue";
import Tasks from "../components/Tasks.vue";

export default {
  name: "Home",
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
      this.tasks = [ taskObj,...this.tasks];
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
    deleteAll(){
      let confirmation = confirm("Do you really want to delete all tasks?")
      if(confirmation){
        this.tasks = [];
      }
    }
  },
  computed: {
    setToLocalStorage: function () {
      localStorage.setItem("tasks", JSON.stringify(this.tasks));
      return "Setted";
    },
  },
  created() {
    this.tasks = this.tasksArr || this.tasksArr == [] ? this.tasksArr : [];
    this.taskId = this.tasks.length>0? (this.tasks[0].id)+1: 1
  },
};
</script>
