<template>
  <div class="">
    <v-text-field
      v-model="newTaskTitle"
      @click:append="addTask"
      @keyup.enter="addTask"
      class="pa-3"
      outlined
      label="Add task"
      append-icon="mdi-plus"
      hide-details
      clearable
    >
    </v-text-field>
    <v-main>
    <v-list
      flat class="pa-3"
    >
    <div v-for="task in tasks"
          :key="task.id">
      <v-list-item
        @click="doneTask(task.id)"
        :class="{ 'blue lighten-5' : task.done}"
        >
          <template v-slot:default>
            <v-list-item-action>
              <v-checkbox :input-value="task.done"></v-checkbox>
            </v-list-item-action>

            <v-list-item-content>
              <v-list-item-title
                :class="{ 'text-decoration-line-through' : task.done}"
              >
                {{ task.title }}</v-list-item-title>
            </v-list-item-content>

            <v-list-item-action>
            <v-btn
             @click.stop="deleteTask(task.id)"
             icon
            >
              <v-icon color="primary lighten-1">mdi-delete</v-icon>
            </v-btn>
          </v-list-item-action>
          </template>

          
        </v-list-item>
        
    </div>


    </v-list>
    </v-main>
    </div>

</template>

<script>
 export default {
   data(){
     return{
       newTaskTitle:'',
       tasks: [
       ]
     }
   },
   methods:{
     addTask(){
       let newTask = {
         id: Date.now(),
         title: this.newTaskTitle,
         done: false
       }
       this.tasks.push(newTask);
       this.newTaskTitle = ''
     },
     doneTask(id){
       let task = this.tasks.filter(task => task.id === id)[0]
       task.done = !task.done
     },
     deleteTask(id){
       this.tasks = this.tasks.filter(task => task.id !== id)
     }
   }
 }
    
</script>
