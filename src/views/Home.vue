<template>
  <div id="app">
    <Todos v-bind:todos="todos" v-on:del-todo="deleteTodo" class="todos"/>
    <!-- <AddTodo v-on:add-todo="addTodo" /> -->
  </div>
</template>

<script>
import Todos from '../components/Todos'
// import AddTodo from '../components/AddTodo'
import axios from 'axios'

export default {
  name: 'Home',
  components: {
    Todos,
    // AddTodo
  },
  data(){
    return{
      todos: []
    }
  },
  methods: {
    deleteTodo(id){
      // axios.delete(`https://jsonplaceholder.typicode.com/todos/${id}`)
      // .then(res => this.todos = this.todos.filter(todo => todo.id !== id))
      // .catch(err => console.log(err));
     this.todos = this.todos.filter(todo => todo.id !== id);
    },
    addTodo(newTodo){
      const {title, completed } = newTodo;

      axios.post('https://jsonplaceholder.typicode.com/todos', {
        title,
        completed
      })
      .then(res => this.todos = [...this.todos, res.data])
      .catch(err => console.log(err));

    }
  },
  //Get sample data from jsonplaceholder
  created(){
    axios.get('https://jsonplaceholder.typicode.com/todos?_limit=4')
    .then(res => this.todos = res.data)
    .catch(err => console.log(err));
  }
}
</script>

<style>
*{
  box-sizing: border-box;
  padding: 0;
  margin: 0;
}

body{
  font-family: Arial, Helvetica, sans-serif;
  line-height: 1.4;
}

.btn{
  display: inline-block;
  border: none;
  background: #555;
  color: #fff;
  padding: 7px 20px;
  cursor: pointer;
}

.btn:hover{
  background: #666;
}

.todos{
  margin-top: 20px;
}
</style>
