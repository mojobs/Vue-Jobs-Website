<script>
export default {
data () {
  return{
    name: 'John Doe',
    status : 'inactive',
    tasks : ['Task1', 'Task2', 'Task3', ],
    link:  "https://google.com"
  }
},
methods : {
  toggleStatus() {
    if (this.status ==='active'){
      this.status = 'pending'
    }
    else if (this.status === 'pending'){
      this.staus = 'inactive'
    }
    else{
      this.status = 'active'
    }


  }
}
}
</script>
<template>
  <h1>{{ name }}</h1>
  <p v-if="status === 'active'">User is Active</p>
  <p v-else-if="status === 'pending'">User is Pending</p>
  <p v-else>User is Inactive</p>

  <h3>Tasks:</h3>
  <ul> 
    <li v-for="task in tasks" :key="task">{{task}}</li>  
  </ul>

  <a v-bind:href="link">Google</a>
  <br>

  <button @click="toggleStatus">Change Status</button>
  
</template>

