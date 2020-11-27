<template>
  <div class="box">

    <form @submit.prevent="addNewTodo">
      <h1 class="text-center">Create you own Todo List</h1> 
      <input v-model="newTodo" name="newTodo" placeholder="Create a new to-do..." v-on="addNewTodo" class="text"> <br>
      <button class="button" style="margin:5px">Add New Todo</button> <br>
    </form>
    <button class="button" style="margin:5px" @click="removeAllTodo">Remove All</button> <br>
    <button class="button" style="margin:5px" @click="markAllDone">Mark all done</button> <br>
  

    <ul>
      <li v-for="(todo, index) in todos" :key="todo.id" class="todo">
      <h3 :class="{done: todo.done}" @click="toggleDone(todo)">{{todo.content}}</h3>
      <button class="button" @click="removeTodo(index)">Remove Todo</button>
      </li>
    </ul>
  </div>
</template>


<script>
  import {ref} from 'vue';
  export default {
  setup(){
    const newTodo = ref('');
    const todos = ref([]);

    function addNewTodo() {
      if (newTodo.value == ''){
        alert('Please enter something')
      }else{
        todos.value.push({
      done:false,
      content: newTodo.value
      });
      newTodo.value ='';
      }
    }

    function toggleDone(todo){
      todo.done = !todo.done;
    }

    function removeTodo(index){
      todos.value.splice(index, 1)
    }

    function markAllDone() {
      todos.value.forEach((todo) => todo.done = true);
    }

    function removeAllTodo() {
      todos.value = [];
    }

    return {
    addNewTodo,
    newTodo,
    todos,
    toggleDone,
    removeTodo,
    markAllDone,
    removeAllTodo
    }
  }
}
</script>

<style>
#app {
  font-family: Helvetica, Arial, sans-serif;
  /* -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale; */
  text-align: center;
  color: #fff;
  margin-top: 60px;
}

.todo{
  cursor: pointer;
}

.done{
  text-decoration: line-through;
}

*{
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body{    
  background-image: url('beautiful-color-ui-gradients-backgrounds-roseanna.png');
  font-family: Arial, Helvetica, sans-serif;
  line-height: 1.4;
  background-position: center;
  background-origin: content-box;
  background-size: cover;
  min-height: 100vh;
}

.box{
	position:absolute;
	left:50%;
	top:50%;
	transform: translate(-50%, -50%);
  background-color: rgba(0, 0, 0, 0.89);
	border-radius:3px;
	padding:70px 100px;
} 

.text-center{
  color:#fff;	
  text-transform:uppercase;
  font-size: 23px;
  margin: -50px 0 80px 0;
  display: block;
  text-align: center;
}




.text{
  border:0;
  border-bottom:1px solid #555;  
  background:transparent;
  width:100%;
  padding:8px 0 5px 0;
  font-size:16px;
  color:#fff;
}
 
.text :focus{ 
  border:none;	
  outline:none;
  border-bottom:1px solid #e74c3c;	
}

.button {
  color:#fff;
  background-color:#e74c3c;
  outline: none;
  border: 0;
  color: #fff;
  padding:10px 20px;
  text-transform:uppercase;
  margin-top:20px;
  border-radius:2px;
  cursor:pointer;
  position:relative;
}

.button:hover {
  background-color: #4CAF50; /* Green */
  color: white;
}


</style>
