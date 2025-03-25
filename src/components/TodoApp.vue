<template>
  <div class="container">

  <h2 class="text-center"> Todo App</h2>

  <div class="d-flex">
    <input v-model="task" type="text" placeholder="Enter task" class="form-control">
    <button @click="submitTask()" class="btn-warning rounded-0">Submit </button>
  </div>
  <table class="table table-bordered">
  <thead>
    <tr>
      <th scope="col" class="text-center">Task</th>
      <th scope="col" class="text-center">Status</th>
      <th scope="col" class="text-center">#</th>
      <th scope="col" class="text-center">#</th>
    </tr>
  </thead>
  <tbody>
    <tr v-for="(task, index) in tasks" :key="index">
      <td >
        <span :class="{'finished': task.status === 'finished'}">
        {{ task.name }}
      </span>
     </td>
      <td style="width: 120px">
        <span  @click="changeStatus(index)" class="pointer">
         {{ firstCharUpper(task.status) }}
        </span>
      </td>
      <td >
        <div class="text-center" @click="editTask(index)">
          <span class="pi pi-pencil"></span>
        </div>
      </td>
      <td>
        <div class="text-center" @click="deleteTask(index)">
          <span class="pi pi-trash"></span>
        </div>
      </td>
    </tr>

  </tbody>
</table>

  </div>
</template>

<script >
export default {
  name: 'HelloWord',
  props:{
    msg: String
  },
  data(){
    return {
      task:'New task',
      editedTask : null,
      availableStatuses: [ 'to-do', 'in-progress','finished'],
      tasks:[
        {
          name: 'прес качат',
          status: 'to-do'
        },
        {
          name: 'бегит',
          status: 'in-progress'
        }
      ]
    }
  },
  methods: {
    submitTask() {
      if(this.task.length === 0 ) return;

     if(this.editedTask === null){
      this.tasks.push({
        name: this.task,
        status: 'to-do'
      })
     }else{
      this.tasks[this.editedTask].name = this.task;
      this.editedTask = null;
     }

      this.task = '';
    },
    deleteTask(index){
      this.tasks.splice(index,1);
    },
    editTask(index){
      this.task = this.tasks[index].name;
      this.editedTask = index;
    },
    changeStatus(index){
       let newIndex = this.availableStatuses.indexOf(this.tasks[index].status);
       if(++newIndex > 2) newIndex =0;
       this.tasks[index].status = this.availableStatuses[newIndex];
          },
    firstCharUpper(str){
      return str.charAt(0).toUpperCase() + str.slice(1);
       }

  }
};
</script>

<style scoped>
.pointer {
  cursor: pointer;
}
.finished {
  text-decoration: line-through;
  }
</style>
