<template>
  <div>
    <div v-if="todos.length == 0">
      <h4 style="text-align: center; margin-top: 2em">No todo yet...!</h4>
    </div>
    <div v-else v-for="todo in todos" v-bind:key="todo.id">
      <TodoItem v-bind:todo="todo" v-on:del-todo="$emit('del-todo', todo.id)" />
    </div>
  </div>
</template>

<script>
import TodoItem from "./Todoitem.vue";

export default {
  name: "Todos",
  props: ["todos"],
  components: {
    TodoItem,
  },
};
</script>
