<template>
  <div id="app" class="container-main" >
    
    <div class="centratura" >
      <h1 >Lista di cose da fare</h1>
      <input type="text" v-model="new_task" @keydown.enter="add_task" placeholder="inserire nuova task">
      <button  @click="add_task">inserisci</button>
    </div>
    <div class="m-3 border border-primary" >
      <div v-for="(task,index) in array_task" :key="index" class="prova  ">
        <div class="bottoni">
          <button  @click="copy_task(index)">copiami</button>
        <button class="m-2" @click="delete_task(index)" type="button"  >eliminami</button>
        <button  class="bottone-singolo" v-if="task.modifica"   @click="modify_task(index)">salva </button>
        <button   v-else @click="modify_task(index)">modificami</button>
        </div>
        <input v-if="task.modifica" type="text" v-model="task_da_modificare" class="task"> 
        <div v-else class="task">{{task.task}}</div>
        
      </div>
    </div>
          
    
  </div>
</template>

<script>
 
import 'bootstrap/dist/css/bootstrap.min.css'; 
export default {
  name: 'App',
  data: function () {
    return {
      array_task:[{
                task: 'latte',
                modifica: false
            },
            {
                task: 'uova',
                modifica: false
            }],
      new_task:[],
      task_da_modificare:[]
    }
  },
  methods:{
    add_task(){
      if(this.new_task!=0){
        var task={
                task: this.new_task,
                modifica: false
            }
      this.array_task.push(task);
      this.new_task=[]
      }
      
    },
    copy_task(index){
      var task={
                task: this.array_task[index].task,
                modifica: false
            }
      this.array_task.push(task)
    },
    delete_task(index){
       this.array_task.splice(index,1)
    },
    modify_task(index){
     
      if (this.array_task[index].modifica==true){
        this.array_task[index].modifica=false
        this.array_task[index].task=this.task_da_modificare
      }
      else{
        this.array_task.forEach(element => {
            element.modifica=false
             
        });
        this.array_task[index].modifica=true
        this.task_da_modificare=this.array_task[index].task
      }
    }
  }
  
}
</script>

<style lang="scss">
 .container-main{
    
   width: 80%;
   margin: 50px auto 0;
    
 }
 .task{
  width: 65%;
   
  display: inline-block;
 }
 .bottoni{
   width: 35%;
   
   display: inline-block;
    
 }
 .prova{
   width: 80%;
   margin: 2px auto;
    
 }
 .bottone-singolo{
   min-width: 90px;
 }
 .centratura{
   text-align: center;
 }
  
</style>
