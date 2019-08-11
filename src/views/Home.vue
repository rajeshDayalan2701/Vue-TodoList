<template>
  <div id="app">
    <AddTodo v-on:add-todo="addTodo"/>
    <Todos v-bind:Todos="todos" v-on:del-todo="deleteTodo" v-on:change-completion="handleChanges"/>
    <CompletedTodos v-bind:CompletedTodos="completedTodos" v-on:change-completion="handleChanges"/>
  </div>
</template>

<script>
import Todos from '../components/Todos';
import AddTodo from '../components/AddTodo';
import CompletedTodos from '../components/CompletedTodos';
import axios from 'axios';

export default {
  name: 'Home',
  components: {
    Todos,
    AddTodo,
    CompletedTodos
  },
  data() {
    return {
      todos: [],
      completedTodos: []
    }
  },
  methods: {
    async deleteTodo(id) {
      try {
        const response = await axios.delete(`https://jsonplaceholder.typicode.com/todos/${id}`);
        this.todos = this.todos.filter(todo => todo.id !== id);
      } catch (error) {
        console.log(error);
      }
    },
    async addTodo(todo) {
      try {
        const response = await axios.post('https://jsonplaceholder.typicode.com/todos', todo);
        console.log(response);
        this.todos = [...this.todos, response.data];
      } catch (error) {
        console.log(error);
      }
    },
    handleChanges(todo) {
      if (!todo.completed) {
        this.completedTodos.splice(this.completedTodos.findIndex(todo1 => todo1.id === todo.id), 1);
        this.todos.push(todo);
      } else {
        this.todos.splice(this.todos.findIndex(todo1 => todo1.id === todo.id), 1);
        this.completedTodos.push(todo);
      }
    }
  },
  async created () {
    try {
      const response = await axios.get('https://jsonplaceholder.typicode.com/todos?_limit=5');
      if (response.data) {
        response.data.forEach(todo => {
        (todo.completed) ? this.completedTodos.push(todo) : this.todos.push(todo);
      });
      }
    } catch (error) {
      console.log(error);
    }
  }
}
</script>

<style>
  * {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
  }

  body {
    font-family: Arial, Helvetica, sans-serif;
    line-height: 1.4;
  }

  .btn {
    display: inline-block;
    border: none;
    background: #555;
    color: #fff;
    padding: 7px 20px;
    cursor: pointer;
  }

  .btn:hover {
    background: #666;
  }
</style>
