<template>
  <div class="todo" >
    <v-list
      flat
      three-line
    >
      <v-subheader>General</v-subheader>
        <v-list-item
        @click="doneTask(task.id)"
        :class="{'blue lighten-5' : task.done}"
        v-for="task in tasks" 
        :key="task.id"
        >
    
          <template v-slot:default>
            <v-list-item-action>
              <v-checkbox 
              :input-value="task.done">
              </v-checkbox>
            </v-list-item-action>

            <v-list-item-content>
              <v-list-item-title :class="{'text-decoration-line-through' : task.done}">{{task.title}}</v-list-item-title>
              <v-list-item-subtitle>{{task.subtitle}}</v-list-item-subtitle>
            </v-list-item-content>

          <v-menu
            bottom
            left
          >
            <template v-slot:activator="{ on, attrs }">
              <v-btn
                icon
                v-bind="attrs"
                v-on="on"
              >
                <v-icon>mdi-dots-vertical</v-icon>
              </v-btn>
            </template>
            <v-list>
              <v-list-item
              >
              <v-list-item-action>
                <v-dialog
                  v-model="dialog"
                  max-width="500px"
                  max-height="700px"
                >
              <template v-slot:activator="{ on, attrs }"> 
              <v-btn 
                icon
                v-bind="attrs"
                v-on="on"
              >
                  <v-icon color="grey lighten-1">mdi-magic-staff</v-icon>
              </v-btn>
               </template>
               <v-card >
                  <v-subheader class="font-weight-medium" >Edit Task</v-subheader>
                  <v-card-text>
                      <v-text-field
                        v-model="TaskTitle"
                        label="Title"
                        clearable
                      >
                      </v-text-field>
                      <v-text-field
                      v-model="TaskSubtitle"
                      label="Subtitle"
                      clearable
                      >
                      </v-text-field>
                      <v-card-actions>
                      <v-spacer></v-spacer>
                      <v-btn
                      text
                      color="primary"
                      @click="editTask"
                      >
                      Submit
                      </v-btn>
                      </v-card-actions>
                      </v-card-text>
                      </v-card>
                      </v-dialog>
              </v-list-item-action>
              <v-list-item-action>
              <v-btn 
                @click.stop="deleteTask(task.id)"
               icon>
                  <v-icon color="grey lighten-1">mdi-nuke</v-icon>
              </v-btn>
            </v-list-item-action>
              </v-list-item>
            </v-list>
          </v-menu>
          </template>
        </v-list-item>
    </v-list>
    <v-container fluid>       
      <v-dialog
      v-model="dialog"
      max-width="500px"
      max-height="700px"
      >
      <template v-slot:activator="{ on, attrs }"> 
            <v-btn 
              slot = "activator" 
              fab
              color="accent"
              elevation="9"
              absolute
              :style="{bottom: '10%', left: '85%', transform:'translateX(-50%)'}"
              bottom
              v-bind="attrs"
              v-on="on"
            >
            <v-icon>mdi-plus</v-icon>
            </v-btn>
            </template>
        <v-card >
        <v-subheader class="font-weight-medium" >Add Task</v-subheader>

          <v-card-text>
            <v-text-field
            v-model="newTaskTitle"
            label="Title"
            clearable
          >
          </v-text-field>
          <v-text-field
            v-model="newTaskSubtitle"
            label="Subtitle"
            clearable
          >
          </v-text-field>
             <v-card-actions>
              <v-spacer></v-spacer>
              <v-btn
                text
                color="primary"
                @click="addTask"
                @keyup.enter="addTask"
              >
                Submit
              </v-btn>
            </v-card-actions>
          </v-card-text>
          </v-card>
        </v-dialog>
     </v-container>
  </div>
</template>

<script>
  export default {
    name: 'Home',
    data(){
      return{
        edittedTaskTitle: '',
        edittedTaskSubtitle: '',
        newTaskTitle: '',
        newTaskSubtitle: '',
        tasks:[
          {
            id: 1,
            title: 'Notifcations',
            subtitle: 'Notify me about updates to apps or games that I downloaded',
            done: false
          },
          {
            id: 2,
            title: 'Super',
            subtitle: 'updates to apps or games that I downloaded',
            done: false
          },
          {
            id: 3,
            title: 'Man',
            subtitle: ' apps or games that I downloaded',
            done: false
          }
        ]
      }
    },
    methods: {
      doneTask(id){
        let task = this.tasks.filter(task => task.id == id)[0]
        task.done = !task.done
      },
      deleteTask(id){
        this.tasks = this.tasks.filter(task => task.id !== id)
      },
      addTask(){
        let newTask = {
          id: Date.now(),
          title: this.newTaskTitle,
          subtitle: this.newTaskSubtitle,
          done: false
        }
        this.tasks.push(newTask)
        this.newTaskTitle = ''
        this.newTaskSubtitle = ''
      },
      editTask(){
          console.log("Task Editted")
        }
         }
        }

  
</script>
