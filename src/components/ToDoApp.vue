<script>
export default
{
  name: "ToDoApp",
  data()
  {
    return {
      task: '',
      editTask: '',
      updateStatus: [ 'kész', 'halasztás', 'elvégezendő'],
      tasks: [
        {
          name: 'Tanulni a matekot',
          status: 'elvégzendő'
        },
        {
          name: 'Bolta menni',
          status: 'kész'
        },
      ]
    }
  },
  methods:{
    addNew(){
     if(this.task.length === 0) return;
      if(this.editTask === null){ 
      this.tasks.push({
        name: this.task,
        status: 'elvégzendő'
      });
    }else{
      this.tasks[this.editTask].name = this.tasks;
      this.editTask = null;
    }

     this.task = '';
    },
    deletTask(t){
    this.tasks.splice(t, 1);
  },
  editTask(t){
    this.task = this.tasks[t].name;
    this.editTask = t;
  },
  change(t){
   let newStatus = this.updateStatus.indexOf(this.tasks[t].status);
   if(++newStatus > 2) newStatus = 0;
   this.tasks[t].status = this.updateStatus[newStatus];

  }
  }
}
   

</script>

<template>
  <div class="container">
    <h2 class="text-center mt-4 bg-warning">Vuede sok feladat</h2>
  </div>

  <!--input-->
  <div class="d-flex">
    <input v-model="task" type="text" placeholder="Írd mi a dolog!" class="form-control">
    <button @click="addNew" class="btn btn-danger">Hozzáad</button>
  </div>
  
  <!--table-->
  <table class="table table-bordered mt-2">
  <thead>
    <tr>
      <th scope="col">Feladat</th>
      <th scope="col">Státusz</th>
      <th scope="col" class="text-center">#</th>
      <th scope="col" class="text-center">#</th>
    </tr>
  </thead>
  <tbody>
    <tr v-for="(task, t) in tasks" :key="t">
      <td>{{task.name}}</td>
      <td style=" width 120px">
        <span @click="change(t)" class="updateStatus">
          {{ task.status }}
        </span>
      </td>
      <td>
        <div class="text-center" @click="deletTask(t)">
          <span>
            <svg xmlns="http://www.w3.org/2000/svg"  width="16" height="16" fill="currentColor" class="bi bi-trash-fill" viewBox="0 0 16 16">
              <path d="M2.5 1a1 1 0 0 0-1 1v1a1 1 0 0 0 1 1H3v9a2 2 0 0 0 2 2h6a2 2 0 0 0 2-2V4h.5a1 1 0 0 0 1-1V2a1 1 0 0 0-1-1H10a1 1 0 0 0-1-1H7a1 1 0 0 0-1 1H2.5zm3 4a.5.5 0 0 1 .5.5v7a.5.5 0 0 1-1 0v-7a.5.5 0 0 1 .5-.5zM8 5a.5.5 0 0 1 .5.5v7a.5.5 0 0 1-1 0v-7A.5.5 0 0 1 8 5zm3 .5v7a.5.5 0 0 1-1 0v-7a.5.5 0 0 1 1 0z"/>
          </svg>
          </span>
        </div>
      </td>
      <td>
        <div class="text-center" @click="editTask(t)">
          <span>
            <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-pencil-fill" viewBox="0 0 16 16">
                <path d="M12.854.146a.5.5 0 0 0-.707 0L10.5 1.793 14.207 5.5l1.647-1.646a.5.5 0 0 0 0-.708l-3-3zm.646 6.061L9.793 2.5 3.293 9H3.5a.5.5 0 0 1 .5.5v.5h.5a.5.5 0 0 1 .5.5v.5h.5a.5.5 0 0 1 .5.5v.5h.5a.5.5 0 0 1 .5.5v.207l6.5-6.5zm-7.468 7.468A.5.5 0 0 1 6 13.5V13h-.5a.5.5 0 0 1-.5-.5V12h-.5a.5.5 0 0 1-.5-.5V11h-.5a.5.5 0 0 1-.5-.5V10h-.5a.499.499 0 0 1-.175-.032l-.179.178a.5.5 0 0 0-.11.168l-2 5a.5.5 0 0 0 .65.65l5-2a.5.5 0 0 0 .168-.11l.178-.178z"/>
            </svg>
          </span>
        </div>
      </td>
    </tr>
  </tbody>
</table>
  

  </template>


<style scoped>
.updateStatus
{
  cursor: pointer;
}

</style>
