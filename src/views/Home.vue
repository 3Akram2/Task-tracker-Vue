<template>
    <div  v-if="showAddTask">
    <AddTask @add-task="addTask"/>
  </div>
    <Tasks @toggle-reminder='toggleReminder' @delete-task="deleteTask" :tasks="tasks" />
  
</template>
<script>
import AddTask from "../components/AddTask.vue"
import Tasks from "../components/Tasks.vue"
export default{
    props:{
showAddTask:Boolean,
    },
    components:{
        Tasks,
        AddTask,
    },
    data()
    {return{
        tasks:[]
    }
    },
    
    methods:{
   
    async addTask(task){
      const res =await fetch('api/tasks',{
        method: 'POST',
        headers:{
          'content-type':'application/json',
        },
        body: JSON.stringify(task)
      });
      
      this.tasks = [...this.tasks,task]
    },
    async deleteTask(id){
      if(confirm('Are you sure?')){
        const res = await fetch(`api/tasks/${id}`,
        {
          method: 'DELETE',

        })
        console.log(res.status)

        res.status === 200 ?( this.tasks=this.tasks.filter((task)=>task.id !==id)):alert('error deleting task')
      }
      
    },
    async toggleReminder(id) {
      const taskToToggle = await this.fetchTask(id)
      const updTask = { ...taskToToggle, reminder: !taskToToggle.reminder }
      const res = await fetch(`api/tasks/${id}`, {
        method: 'PUT',
        headers: {
          'Content-type': 'application/json',
        },
        body: JSON.stringify(updTask),
      })
      const data = await res.json()
      this.tasks = this.tasks.map((task) =>
        task.id === id ? { ...task, reminder: data.reminder } : task
      )
    },
    async fetchTasks(){
      const res = await fetch('api/tasks')
      const data = await res.json()
      return data
    },
    async fetchTask(id){
      const res = await fetch(`api/tasks/${id}`)
      const data = await res.json()
      return data
    }
   
  },
  async created(){
    this.tasks = await this.fetchTasks()
  }
}


</script>