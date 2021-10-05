<template>
    <div class="card">
        <form @submit.prevent="newTask">
        <input type="text" v-model="text" class="addTaskInput">
        <br>
        <div style="display: flex; flex-wrap: none; justify-content: around;">
        <input type="datetime-local" v-model="datetime" class="addTaskInput">
        <!-- <input type="time" v-model="time" class="addTaskInput"> -->
        </div>
        <br>
        <input type="checkbox" style="margin-right:8px;" v-model="reminder"  id="check">
        <label for="check">Reminder</label>
        <br>
          <button class="btn" type="submit"> <i class="fa fa-floppy-o"></i> Save Task</button>
        </form>
    </div>
</template>

<script>

export default {
    name: "AddTask",
    props: {
        taskId: Number
    },
    data(){
        return{
            text: "",
            reminder: false,
            datetime: "",
            taskObj: {}
        }
    },
    methods:{
        newTask(){
            if(this.text === "" || this.text.length <3){
                alert("Can't add empty field or less than 3 characters")
                return
            }
            if(this.datetime === ""){
                this.datetime = Date.now()
            }
            this.taskObj = {
                id: this.taskId,
                text: this.text,
                reminder: this.reminder,
                datetime: this.datetime
            }
            this.$emit("add-task", this.taskObj)
            this.text = ""
            this.reminder = false
            this.datetime = ""
            // this.time = null
        }
    }
}
</script>

<style scoped>
.addTaskInput{
    width: -webkit-fill-available;
    padding: 5px 11px;
    font-size: 24px;
    font-family: inherit;
    border-radius: 38px;
    outline: none;
    border: 2px dashed cornflowerblue;
    margin: 14px 14px;
    background: #F3F2F6;
    max-width: 100%;
}
.addTaskInput:hover , .addTaskInput:focus{
    background: white;
}

</style>