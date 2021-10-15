<template>
  <form @submit.prevent="addTask">
    <input
      type="text"
      placeholder="Enter task"
      class="form-control my-2 mb-3"
      v-model.trim="text"
    />
    <button class="btn btn-success w-100 mb-5">Add</button>
  </form>
</template>

<script>
import { ref, inject } from "vue";
export default {
  setup() {
    const text = ref("");

    const tasks = inject("tasks");
    
    const addTask = () => {
      if (text.value === "") {
        return console.log("texto vacio");
      }
      const task = {
        text: text.value,
        status: false,
        id: Date.now(),
      };
      tasks.value.push(task);
      text.value = "";
    };
    return { addTask, text };
  },
};
</script>

<style>
.btn{
  font-weight: bold;
}
</style>