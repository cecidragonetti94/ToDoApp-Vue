<template>

<h1 class="text-center mb-5">To do List 📃</h1>
    <Form/>
    <TaskItem v-for="task in tasks" :key="task.id" :task="task"/>
<div class="alert alert-dark mt-3 " v-if="tasks.length === 0">No pending tasks 😀</div>

</template>

<script>
import Form from './Form.vue'
import TaskItem from './TaskItem.vue'
import {ref,provide, watchEffect} from 'vue'
export default {
components:{
    Form,
    TaskItem,
},
setup(){
    const tasks = ref([])
    provide('tasks', tasks)
    
    if(localStorage.getItem('tasks')){
        tasks.value = JSON.parse(localStorage.getItem('tasks')) //ejecuta el if empuja las tareas q estan en local..
        //y cada vez que se modifiquen o elimine lo va guardando sirve para cuando actualizo la pag que no se borre todo
    }

    watchEffect(() =>{
        localStorage.setItem('tasks', JSON.stringify(tasks.value))
    })
    
    return {tasks}
}
}
</script>

<style>
h1{
    color:rgb(11, 109, 24);
    font-weight: bolder;
    font-size: 40px;
}
</style>