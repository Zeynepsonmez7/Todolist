<template>
  <div  class = "container">
   <h2 class=" text-center mt-5">My Vue Todo App</h2>
     <div class="d-flex ">
      <input v-model= "task" type= "text"  placeholder= "Enter task"  style=  "width: 700px;" >
     <button style="margin:12px;" @click="submitTask"  class="btn btn-danger rounded-25">SUBMİT</button>
     <button style="margin:12px;" @click= "handleClick('to-do')" class="btn btn-danger rounded-25">TO DO</button>
     <button  style="margin:12px;" @click= "handleClick('in-progress')" class="btn btn-danger rounded-25">İN PROGRESS</button>
     <button style="margin:12px ;" @click= "handleClick( 'finished')" class="btn btn-danger rounded-25">FİNİSHED</button>
     <button style="margin:12px ;" @click="clear()"  class="btn btn-danger rounded-25">Fılter</button>
    </div>

  
  
  <table class="table table-bordered mt-5">
  <thead>
    <tr>
      <th scope="col">Task</th>
      <th scope="col">Status</th>
      <th scope="col" class = "text-center">#</th>
      <th scope="col" class = "text-center">#</th>
    </tr>
  </thead>
  <tbody>
    <tr v-for="(task,index) in filteredTasks" :key="index">
      <td>
        <span :class  = " {'finished': task.status ==='finished'}">{{task.name}}</span> </td>
      <td style = "widht: 120px">
        <span @click="changeStatus (index)" class = "pointer" :class= "{'text-danger': task.status ===   'to-do' , 
        'text-warning': task.status === 'in-progress' ,
        'text-warning': task.status ===   'finished' 
        }  "
        
        >
        
        {{firstCharUpper(task.status)}}</span></td>
      <td >
        
        <div class ="text-center" @click="editTask(index)">
        <span class=" fa fa-pen"> </span>
         
        </div>
      </td>
      <td>
        <div class="text-center" @click="deleteTask(index)">
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
  name: 'TodoApp',
  props: {
    msg: String,
  },
  data(){
    return {
      task:'',
      editedTask:null,
      availableStatuses: [ 'to-do', 'in-progress','finished'],
      filteredTasks : [],

      tasks: [
        {
          name: 'Steal bananas from the store ',
          status:'to-do'
        },
        { 
         name: 'Eat 1 kg chocolata in 1 hour.',
          status:'in-progress'
        },
         {
          name: 'Steal bananas from the store ',
          status:'to-do'
        },
        { 
         name: 'Eat 1 kg chocolata in 1 hour.',
          status:'in-progress'
        },
         {
          name: 'Steal bananas from the store ',
          status:'to-do'
        },
        { 
         name: 'Eat 1 kg chocolata in 1 hour.',
          status:'in-progress'
        },
        {
          name: 'Steal bananas from the store ',
          status:'to-do'
        },
        { 
         name: 'Eat 1 kg chocolata in 1 hour.',
          status:'in-progress'
        }
      ],
    }
  },
mounted (){
  this.filteredTasks = this.tasks;
},

methods: {
clear(){
  this.filteredTasks= this.tasks;

},

  handleClick(status){
    this.filteredTasks = this.tasks.filter(item =>item.status === status);
  },
  submitTask(){
  
   if(this.task.length === 0) return;
if(this.editedTask ===null){
  this.tasks.push(
    {
      name: this.task,
      status:'to-do'
    }
  );
  }else{
    this.tasks[this.editedTask].name=this.task;
this.editedTask=null;
  }
 
   this.task =  '';
  },
  


 
 deleteTask(index){
    this.tasks.splice(index,1);
  
  },
  editTask(index){
    this.task =this.tasks[index].name;
    this.editedTask = index;
  },
  changeStatus(index){
   let newIndex = this.availableStatuses.indexOf(this.tasks[index].status);
if(++newIndex > 2) newIndex = 0;
this.tasks [index].status = this.availableStatuses[newIndex];

  },
firstCharUpper(str){
  return str.charAt(0).toUpperCase() + str.slice(1);
}

  }};
  
  </script>


<style scoped>
.pointer{
  cursor:pointer;
}
.finished {
  text-decoration: line-through;
}
td {
  transition: 100ms all;
}
td:hover {
  background-color:antiquewhite;
  cursor: pointer;
}
div {
  background-color:aliceblue;
}





</style>
