<template>
  <header>
    <center><h1>TODO APP</h1></center>
  </header>
  <div class="todo-container">
    <form v-on:submit.prevent="onSubmit">
      <input v-model="newTodo" type="text" placeholder="Type here..." class="todo-input" />
      <button @click="addTodo()" class="add-btn">ADD</button>
    </form>
    
    <ul class="todo-list">
      <div class="todo" v-for="todo in todos" :key="todo.id" v-bind:class="{ 'completed': todo.check }">
      <li>{{todo.title}}</li>
      <button class="edit" @click="editTodo(todo)">Edit</button>
      <button class="check" @click="checkTodo(todo)">Done</button>
      <button class="delete" @click="deleteTodo(todo)">Delete</button>
    </div>
    </ul>
  </div>
</template>

<script>
export default {
  data(){
    return{
      newTodo : '',
      todos: []
    }
  },

methods:{
  addTodo(){
    this.todos.push({id:this.todos.length, title: this.newTodo, check: false});
    this.newTodo = '';
    localStorage.setItem("storage", JSON.stringify(this.todos));
  },

  deleteTodo(todo){
    this.todos.splice(this.todos.indexOf(todo), 1);
    localStorage.setItem("storage", JSON.stringify(this.todos));
  },

  editTodo(todo){
    this.deleteTodo(todo);
    this.newTodo = todo.title;
  },

  checkTodo(todo){
    if(todo.check == false){
      todo.check = true;
      localStorage.setItem("storage", JSON.stringify(this.todos));
  }else{
    todo.check = false;
    localStorage.setItem("storage", JSON.stringify(this.todos));
  }
  }

},

created: function(){
  this.todos = JSON.parse(localStorage.getItem("storage" || []))
}

}
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Poppins:ital,wght@0,100;0,200;0,300;0,400;0,500;0,600;0,700;0,800;0,900;1,100;1,200;1,300;1,400;1,500;1,600;1,700;1,800;1,900&display=swap");

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: "Poppins", sans-serif;
}
body {
  background: linear-gradient(120deg, rgb(201, 223, 233), rgb(104, 180, 216));
  height: 100vh;
  width: 100vw;
  padding: 10vmin 5vmin;
}
.todo-container {
  width: 100%;
  margin: 0 auto;
}
form {
  display: flex;
  border-radius: 0.5rem;
  height: 40px;
  margin: 20px 0;
}
.todo-input {
  flex: 5;
  width: 100%;
  background-color: white;
  border: none;
  padding: 0 10px;
  color: black;
  border-radius: 0.5rem 0 0 0.5rem;
}
.add-btn {
  flex: 1;
  width: 100%;
  padding: 2px;
  border: none;
  background-color: rgb(26, 93, 156);
  border-radius: 0 0.5rem 0.5rem 0;
  color: white;
}

.todo {
  display: flex;
  align-items: center;
  background-color: white;
  margin: 10px 0;
  border-radius: 0.5rem;
}
.completed {
  opacity: 0.5;
}
.edited {
  transform: translateY(-5rem);
  opacity: 0;
  transition: 0.5s;
}
.deleted {
  transform: translateY(10rem) rotateZ(-20deg);
  opacity: 0;
  transition: 0.5s;
}
.completed > li {
  text-decoration: line-through;
}
.todo li {
  width: 100%;
  list-style: none;
  padding: 0 10px;
}
.check,
.delete,
.edit {
  padding: 15px 10px;
  border: none;
  color: white;
}
.edit {
  background-color: rgb(26, 93, 156);
}
.check {
  background-color: rgb(72, 126, 51);
}
.delete {
  background-color: rgb(192, 73, 73);
  border-radius: 0 0.5rem 0.5rem 0;
}

@media (min-width: 40em) {
  body {
    padding: 10vmin 30vmin;
  }
}
@media (min-width: 70em) {
  body {
    padding: 10vmin 60vmin;
  }
}
</style>
