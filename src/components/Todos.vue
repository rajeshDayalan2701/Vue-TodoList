<template>
  <div>
    <div v-bind:key="todo.id" v-for="todo in Todos">
      <TodoItems v-bind:todo="todo" v-on:del-todo="$emit('del-todo', todo.id)"/>
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
    props: ["Todos"]
  }
</script>

<style scoped>

</style>
