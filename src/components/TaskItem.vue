.<template>
  <div class="alert alert-warning mt-3 d-flex justify-content-between align-item-center">
      <p class="mb-0" :class="{'tach': task.status}">{{task.text}}</p>
      <div>
          <i class="fas fa-undo-alt mx-2 text-success" v-if="task.status"></i>
          <i class="fas fa-check-circle mx-2 text-success " v-else role="button" @click="change(task.id)"></i>
          <i class="fas fa-minus-circle text-danger" role="button" @click="remove(task.id)"></i>
      </div>
  </div>
</template>

<script>
import { inject } from '@vue/runtime-core'
export default {
props: {
    task:{
        type:Object,
        required: true
    }
},
setup(){
    const tasks = inject('tasks')
    const remove = id => {
       tasks.value = tasks.value.filter(item => item.id !== id) //cuandose igual no vamos a devolver el item
    }
    const change = id => {
        tasks.value = tasks.value.map(item =>{
            if(item.id === id){
                item.status = !item.status
            }
            return item
        })
    }
    return {remove,change}
}
}
</script>

<style scoped>
.tach{
    text-decoration: line-through;
}
</style>