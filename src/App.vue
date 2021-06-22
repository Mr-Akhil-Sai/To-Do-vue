<template>
  <div class="container">
    <h2 class="h2 text-center mt-5">To Do</h2>
    <div class="d-flex">
      <input type="text" v-model="task" name="task" id="task" class="form-control rounded-0">
      <button @click="submitTask" class="btn btn-warning rounded-0">Submit</button>
    </div>
    <table class="table table-bordered mt-5">  
  <thead>
    <tr>
      <th scope="col">Task</th>
      <th scope="col">Status</th>
      <th scope="col">Edit</th>
      <th scope="col">Delete</th>
    </tr>
  </thead>
  <tbody>
    <tr v-for="(task,index) in tasks" :key="index">
      <td ><span>{{ task.name }}</span></td>
      <td>{{task.status}}</td>
      <td>
        <div class="text-center" @click="editTask(index)"> 
          <span class="fa fa-pen"></span>
        </div>
        </td>
      <td><div class="text-center" @click="deleteTask(index)"> 
          <span class="fa fa-trash"></span>
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
          status: "To-Do"
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
    }
  }
}
</script>

