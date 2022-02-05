<template>
  <div class="todo-item">
    <p v-bind:class="{ 'is-complete': todo.completed }">
      <input
        :id="todo.id"
        type="checkbox"
        :checked="todo.completed"
        v-on:change="markComplete(todo.id)"
      />
      <label :for="todo.id">{{ todo.title }}</label>
    </p>
    <button v-on:click="$emit('del-todo', todo.id)" class="del">X</button>
  </div>
</template>

<script>
export default {
  name: "TodoItem",
  props: ["todo"],
  methods: {
    markComplete(id) {
      this.todo.completed = !this.todo.completed;
      fetch(`http://localhost:3000/todos/${id}`, {
        method: "PUT",
        headers: {
          "Content-Type": "application/json",
        },
        body: JSON.stringify(this.todo),
      })
        .then((response) => {
          if (!response.ok) {
            console.error("Error:", response.json());
          }
          return response.json();
        })
        .then((data) => {
          console.log("Success:", data);
        })
        .catch((error) => {
          console.error("Error:", error);
        });
    },
  },
};
</script>

<style scoped>
.todo-item {
  background: #f4f4f4;
  padding: 0.8rem 1.2em;
  border-bottom: 1px dotted #ccc;
  display: flex;
  justify-content: space-between;
}

.todo-item p > label {
  margin: 0 1em;
}

.is-complete {
  text-decoration: line-through;
}

.del {
  background: #f00;
  color: #fff;
  border: none;
  padding: 0 1.5em;
  border-radius: 5px;
  cursor: pointer;
  /* float: right; */
}
</style>