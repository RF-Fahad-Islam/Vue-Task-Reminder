<template>
  <div :class="[task.reminder ? 'reminder' : 'task', 'card']" @dblclick="toggleReminderEmit(task.id)" style="text-align: left">
    <button @click="$emit('delete-task', task.id)"><i class="fa fa-times"></i></button>
    <div class="text">
      <h3>{{ task.text }}</h3>
      <p> <i class="fa fa-calendar"></i> {{ new Date(task.datetime).toLocaleDateString("en", options) }}<br> <i class="fa fa-clock-o"></i> {{ new Date(task.datetime).toLocaleTimeString('en-US') }}</p>
    </div>
  </div>
</template>

<script>
export default {
  name: "Task",
  props: {
    task: Object,
  },
  data(){
      return {
          options:{ weekday: 'long', year: 'numeric', month: 'long', day: 'numeric' }
      }
  },
  methods: {
      toggleReminderEmit(id){
          this.$emit("toggle-reminder", id)
      }
  }
};
</script>

<style scoped>
* {
  text-overflow: initial;
}
.text {
  margin-left: 10px;
}
.reminder{
    border: 2px solid red!important;;
    border-left: 9px solid red!important;
  padding: 10px 10px!important;
}
h3 {
    margin-bottom: 8px;
  overflow: auto;
}
.task {
  border: 2px solid black!important;
    border-left: 9px solid #4d4949!important;
    padding: 10px 10px!important;
}
button {
  position: relative;
  /* top: 18px; */
  float: right;
  background: none;
  font-size: 20px;
  border: none;
  cursor: pointer;
}

button:hover {
  color: red;
}
</style>