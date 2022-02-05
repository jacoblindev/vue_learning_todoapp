<template>
  <div>
    <AddTodo v-on:add-todo="addTodo" />
    <Todos v-bind:todos="todos" v-on:del-todo="deleteTodo" />
  </div>
</template>

<script>
import Todos from "../components/Todos";
import AddTodo from "../components/AddTodo";
// import axios from "axios";

export default {
  name: "Home",
  components: {
    Todos,
    AddTodo,
  },
  data() {
    return {
      todos: [],
    };
  },
  methods: {
    deleteTodo(id) {
      fetch(`http://localhost:3000/todos/${id}`, {
        method: "DELETE",
      })
        .then((response) => {
          if (!response.ok) {
            console.error("Error:", response.json());
          }
          return response.json();
        })
        .then((data) => {
          console.log("Success:", data);
          this.getTodos();
        })
        .catch((error) => {
          console.error("Error:", error);
        });
      //   axios
      //     .delete(`https://jsonplaceholder.typicode.com/todos/${id}`)
      //     .then((this.todos = this.todos.filter((e) => e.id !== id)))
      //     .catch((err) => console.log(err));
    },
    addTodo(newTodo) {
      fetch("http://localhost:3000/todos", {
        method: "POST",
        headers: {
          "Content-Type": "application/json",
        },
        body: JSON.stringify(newTodo),
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

      //   const { title, completed } = newTodo;
      //   axios.post('https://jsonplaceholder.typicode.com/todos', {
      //     title,
      //     completed
      //   })
      //     .then(res => this.todos = [...this.todos, res.data])
      //     .catch(err => console.log(err));

      this.todos = [...this.todos, newTodo];
    },
    getTodos() {
      fetch("http://localhost:3000/todos")
        .then((response) => response.json())
        .then((data) => (this.todos = data));
    },
  },
  created() {
    // axios
    //   .get("https://jsonplaceholder.typicode.com/todos?_limit=6")
    //   .then((res) => (this.todos = res.data))
    //   .catch((err) => console.log(err));
  },
  mounted() {
    this.getTodos();
  },
};
</script>

<style>
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  font-family: Helvetica, sans-serif;
  line-height: 1.5;
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
  background: #777;
}
</style>
