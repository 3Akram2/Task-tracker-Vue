<template>
    <header>
        <h1>{{title}}</h1>
        <Button
         v-show="homePage" 
         @toggle-add-task= "$emit('toggle-add-task')" :color="ShowAddTask?'red':'green'" :btext="ShowAddTask ? 'Close':'Add Task'" />
    </header>
</template>
<script>
import Button from "./Button.vue";
export default {
    name: "Header",
    props: {
        title:String,
        ShowAddTask: Boolean
    },
    components :{
        Button
    },
    computed:{
        homePage(){
            if (this.$route.path === '/'){
            return true               
            }
            else{
                return false
            }
        }
    },
    emits:['toggle-add-task'],
}
</script>
<style scoped>
header{
    display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 20px;
    
}
</style>