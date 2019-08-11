<template>
  <div>
    <p v-if="!Todos.length">Hurray!!!! All tasks for today are completed. Go out and have some life.</p>
    <div v-bind:key="todo.id" v-for="todo in Todos">
      <TodoItems v-bind:todo="todo" v-on:change-completion="handleChanges" v-on:del-todo="$emit('del-todo', todo.id)"/>
    </div>
  </div>
</template>

<script>
  import TodoItems from './TodoItems.vue';
  export default {
    name: "Todos",
    components: {
      TodoItems
    },
    props: ["Todos"],
    methods: {
      handleChanges (todo) {
        //On change of the completion status emit to the parent element
        this.$emit('change-completion', todo);
      }
    }
  }
</script>

<style scoped>
  p {
    text-align: center;
    margin: 1rem;
    padding: 0.5rem;
  }
</style>
