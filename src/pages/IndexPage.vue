<template>
  <q-page class="flex flex-center">
   <q-card class="my-card" style="width:600px">
      <q-card-section>
       <div class="text-h4">To-Do List</div>

    </q-card-section>

    <q-card-section>
      <q-card-section>
        <div class="row justify-center">
          <div class="col-12">
            <q-input v-model="todoTask" label="Add Task" >
            <template v-slot:after>
              <q-btn round dense flat icon="send" @click="addItem()"/>
            </template>
            </q-input>
          </div>    
        </div>
         
      </q-card-section>

       

    </q-card-section>
    <q-separator />
    <q-card-section v-if="todoList.length > 0">
       <div class="row justify-center" v-for="(item,index) in todoList" :key=index>
         <div class="col-8 q-py-sm">
             {{ item.value }}
         </div>
         <div class="col-auto q-py-sm">
           <q-btn round dense flat icon="done" @click="DeleteItem(index)"/>
         </div>
          <div class="col-auto q-py-sm">
          </div>
           <q-btn round dense flat icon="update" @click="item.update=!item.update"/>
             <q-input v-if="item.update" v-model="updateTask" label="Update Task"  >
               <template v-slot:after>
                 <q-btn round dense flat icon="send" @click="UpdateItem(index)" />
               </template>
            </q-input>  
       </div>
         
    </q-card-section>
      <q-card-section v-else>
        <div class="row justify-center">
         
            <div class="text-h6">
               Task list is empty
            </div>
         
        </div>
      </q-card-section>
    </q-card>

  </q-page>
</template>

<script>
import { defineComponent } from 'vue'

export default defineComponent({
  name: 'IndexPage',
  data(){
    return {
      todoTask:'',
      updateTask:'',
      todoList:[
        { 
          value:"go to gym",
          update:false 
        },
        { value:"Build an app" , update:false },
        { value:"Next term plannning" , update:false }
      ],
      // update:false 
    }
  },
  methods:{
    addItem(){
      this.todoList.push({ value:this.todoTask }),
      this.todoTask=''
    },
   
    DeleteItem(index){
         this.todoList.splice(index,1)
    },
    UpdateItem(index){
      
      this.todoList[index].value=this.updateTask,
       
      this.update=!this.update
    }
  }
})
</script>
