<script setup>
import { ref, onMounted } from 'vue';

  const name = ref('Gautam');
  const status = ref('inactive');
  const tasks = ref(['Task 1', 'Task 2', 'Task 3']);
  const link = ref('https://www.google.com');
  const newTask = ref('');
  
  const changeStatus = () => {
    status.value = status.value === 'active' ? 'inactive' : 'active';
  }

  const addTask = () => {
    tasks.value.push(newTask.value);
    newTask.value = '';
  }
  
  const removeTask = (task) =>{
    tasks.value = tasks.value.filter(t => t !== task)
  }

  onMounted(async () => {
   const response = await fetch('https://jsonplaceholder.typicode.com/todos');
   const data = await response.json();
   tasks.value = data.map((task) => task.title)
  })


</script>
<template>
  <div>
    <h1>{{ name }}</h1>
    <p v-if="status ==='active'">User is active</p>
    <p v-else>User is inactive</p>
    <form @submit.prevent="addTask">
      <label for="task">Task</label>
      <input type="text" id="task" v-model="newTask" />
      <button type="submit">Add Task</button>
    </form>


    <h2>Tasks</h2>
    <ul>
      <li v-for="task in tasks" :key="task"><span> {{ task }} </span> <button @click="removeTask(task)">x</button></li>
      </ul>
      <a :href="link">Google</a>
      <br>
    </br>
    <button @click="changeStatus">Change Status</button>
  </div>
</template>

