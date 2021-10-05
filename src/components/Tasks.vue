<template>
  <!-- !Show Add Task Button -->
  <button
    class="btn"
    @click="toggleAddTask"
    :style="showAddTask ? { background: '#FF6934' } : {}"
  >
    <i v-if="!showAddTask" style="color: blue" class="fa fa-plus-circle"></i>
    <i v-else style="color: white" class="fa fa-minus-circle"></i>
    {{ showAddTask ? "Close" : "Add Task" }}
  </button>

  <!-- !Form for adding Tasks -->
  <transition
    name="custom-classes-transition"
    enter-active-class="animated bounceInLeft"
    leave-active-class="animated bounceOutRight"
  >
    <AddTask v-if="showAddTask" :taskId="taskId" @add-task="emitTask" />
  </transition>

  <!-- !When There is no task -->
  <transition
    name="custom-classes-transition"
    enter-active-class="animated tada"
    leave-active-class="animated zoomOut"
  >
    <div v-if="tasks.length < 1">
      <div class="card" style="padding: 18px; border-left: 9px solid red">
        <h2>No Tasks</h2>
        <p>Double click a task to mark a task</p>
      </div>
    </div>
  </transition>

  <!-- !Task Cards -->
  <div class="scrollable">
    <div v-for="task in tasks" :key="task.id">
      <Task
        @delete-task="deleteEmit"
        @toggle-reminder="toggleEmit"
        :task="task"
      />
    </div>
  </div>
</template>

<script>
import Task from "./Task";
import AddTask from "./AddTask";

export default {
  name: "Tasks",
  data() {
    return {
      showAddTask: true,
    };
  },
  components: {
    Task,
    AddTask,
  },
  props: {
    tasks: Array,
    taskId: Number
  },
  emits: ["add-task", "toggle-reminder", "delete-task"],
  methods: {
    toggleAddTask() {
      this.showAddTask = !this.showAddTask;
    },
    emitTask(taskObj) {
      this.$emit("add-task", taskObj);
    },
    toggleEmit(id) {
      this.$emit("toggle-reminder", id);
    },
    deleteEmit(id) {
      this.$emit("delete-task", id);
    },
  },
};
</script>

<style>
.card {
  border: 2px dashed rgb(192, 180, 180);
  border-radius: 10px;
  box-sizing: border-box;
  margin-top: 18px;
  padding: 3px;
  box-shadow: 3px 4px 6px rgba(43, 33, 33, 0.5);
}

.scrollable {
  margin-top: 10px;
  border-top: 3px dotted black;
  max-height: 500px;
  overflow-y: scroll;
}

.card:hover {
  box-shadow: 4px 3px 8px black;
}
.btn {
  padding: 9px 25px;
  border-radius: 100px;
  border: none;
  font-size: 21px;
  font-weight: bold;
  font-family: inherit;
  margin: 6px;
}
.btn:hover {
  background-color: #c9c9c9 !important;
  cursor: pointer;
}
</style>
