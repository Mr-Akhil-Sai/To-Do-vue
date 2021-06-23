<template>
  <div class="container">
    <h2 class="h2 text-center mt-5">To Do</h2>
    <div class="d-flex">
      <input type="text" v-model="task" name="task" placeholder="Enter a Task" ref="taskInput" id="task" class="form-control rounded-0">
      <button @click="submitTask" class="btn btn-warning rounded-0">Submit</button>
    </div>
    <table class="table table-bordered mt-5">  
  <thead>
    <tr class="text-center">
      <th scope="col">Task</th>
      <th scope="col" class="operationsWidth">Status</th>
      <th scope="col" class="operationsWidth">Edit</th>
      <th scope="col" class="operationsWidth">Delete</th>
    </tr>
  </thead>
  <tbody>
    <tr v-for="(task,index) in tasks" :key="index">
      <td class="h4" :style="[!task.status? {  textDecoration : 'line-through'}: {}]"><span>{{ task.name }}</span></td>
      <td class="text-center">
        <div @click="taskStatus(index)" v-if="task.status" class="text-success h4">
          <span class="far fa-check-circle" style="cursor: pointer"></span>
        </div>
        <div @click="taskStatus(index)" v-else class="text-danger h4">
          <span class="fas fa-times-circle" style="cursor: pointer"></span>
        </div>
      </td>
      <td>
        <div class="text-center h4" @click="editTask(index)"> 
          <span class="fa fa-pen" style="cursor: pointer"></span>
        </div>
        </td>
      <td><div class="text-center h4" @click="deleteTask(index)"> 
          <span class="fa fa-trash" style="cursor: pointer"></span>
        </div>
        </td>
    </tr>
  </tbody>
</table>
  </div>  
</template>

<script>

export default {
  name: 'App',
  data(){
    return{
      task: "",
      editedTask: null,
    tasks: []
    }
  },
  methods: {
    submitTask(){
      if(this.task.length === 0){
       return alert("enter the task")
      }
      if(this.editedTask === null ){
        this.tasks.push({
          name: this.task,
          status: true
        })
      }
      else{
        this.tasks[this.editedTask].name = this.task
        this.editedTask = null
      }
        this.task = ""
    },
    deleteTask(index){
      this.tasks.splice(index, 1)
    },
    editTask(index){
      this.task = this.tasks[index].name
      this.editedTask = index
      this.$refs.taskInput.focus()
    },
    taskStatus(index){
      if(this.tasks[index].status){
        this.tasks[index].status = false
      }
      else{
        this.tasks[index].status = true
      }
    },
 
  }
}
</script>

<style scoped>
  .operationsWidth{
    width: 150px
  }
@media (max-width: 576px) {
  .operationsWidth{
    width: 10px;
  }
}
</style>

