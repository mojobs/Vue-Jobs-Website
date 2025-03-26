
<template>
<p>{{ name}}</p>
<p> {{ status }}</p>
<form @submit.prevent="addTask">
  <label for="newTask">Add Task</label>
  <input type="text" id="newTask" name="newTask" v-model="newTask">
  <button type="submit">Submit</button>

</form>

<ul>
  <li v-for="(task, index) in tasks" :key ="task"> 
    <span>
      {{task}}
    </span>
    <button @click="deleteTask">x</button>
  </li>
</ul>

<button @click="toggleStatus">Click Me</button>
</template>


<script setup>
import { onMounted, ref } from 'vue'

const name = ref('John Doe')
const status = ref('active')
const tasks = ref(['Task1', 'Task2', 'Task3'])
const newTask = ref('')

const toggleStatus = () => {
    if (status.value ==='active'){
      status.value = 'pending'
    }
    else if (status.value === 'pending'){
      status.value = 'inactive'
    }
    else{
      status.value = 'active'
    }
  };
  const addTask = () => {
    if(newTask.value.trim !== ''){
      tasks.value.push(newTask.value);
      newTask.value = '';
    }
  }
  const deleteTask = (index) => {
    tasks.value.splice(index, 1)
  }

  onMounted(async ()=> {
    try {
    const response = await fetch('https://jsonplaceholder.typicode.com/todos');
    const data = await response.json();
    tasks.value = data.map((task) => task.title)
  } catch(error){
    console.log('Error fetching tasks')

  }
});
</script>