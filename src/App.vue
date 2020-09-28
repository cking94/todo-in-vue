<template class="app">
  <h1>Vue 3 Todo App</h1>
  <form @submit.prevent="addNewTodo">
    <label>New Todo</label>
    <input v-model="newTodo" name="newTodo" />
    <button>Add New Todo</button>
  </form>
  <button @click="markAllAsDone()">Mark All as Done</button>
  <button @click="removeAll()">Remove All</button>
  <ul>
    <li v-for="(todo, index) in todos" v-bind:key="todo.id">
      <h3 :class="{ done: todo.done }" @click="toggleDone(todo)" class="todo">
        {{ todo.content }}
      </h3>
      <button @click="removeTodo(index)">Remove Todo</button>
    </li>
  </ul>
</template>

<script>
import { ref } from "vue";

const newTodo = ref("");
const todos = ref([]);

export default {
  setup() {
    function addNewTodo() {
      todos.value.push({
        id: Date.now(),
        done: false,
        content: newTodo.value,
      });
      newTodo.value = "";
    }

    function toggleDone(todo) {
      todo.done = !todo.done;
    }

    function removeTodo(index) {
      todos.value.splice(index, 1);
    }

    function markAllAsDone() {
      todos.value.forEach((todo) => (todo.done = true));
    }

    function removeAll() {
      todos.value = [];
    }

    return {
      removeAll,
      markAllAsDone,
      removeTodo,
      toggleDone,
      todos,
      newTodo,
      addNewTodo,
    };
  },
};
</script>

<style>
body {
  font-family: sans-serif;
  padding-top: 1em;
  padding-bottom: 1em;
  font-size: 2em;
  width: 80%;
  margin: 0 auto;
}
input,
textarea,
button,
p,
div,
section,
article,
select {
  display: "block";
  width: 100%;
  font-family: sans-serif;
  font-size: 1em;
  margin: 0.5em;
}

.done {
  text-decoration: line-through;
}

.todo {
  cursor: pointer;
}
</style>
