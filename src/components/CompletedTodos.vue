<template>
  <div>
    <h3>Completed Tasks</h3>
    <p v-if="!CompletedTodos.length">No Completed Tasks to show. Hurry up!!!</p>
    <div v-bind:key="todo.id" v-for="todo in CompletedTodos">
      <TodoItems v-bind:todo="todo" v-on:change-completion="handleChanges"/>
    </div>
  </div>
</template>

<script>
import TodoItems from './TodoItems.vue';
export default {
  name: "CompletedTodos",
  props: ["CompletedTodos"],
  components: {
    TodoItems
  },
  methods: {
    handleChanges (todo) {
      //On change of the completion status emit to the parent element
      this.$emit('change-completion', todo);
    }
  }
}
</script>

<style scoped>
  h3 {
    margin-top: 1rem;
    background: #333;
    padding: 0.5rem;
    color: #fff;
    text-align: center;
    font-size: 2rem;
  }
  p {
    text-align: center;
    margin: 1rem;
    padding: 0.5rem;
  }
</style>