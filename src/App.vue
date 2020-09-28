<template>
  <h1>Vue 3 Todo App</h1>

  <form @submit.prevent="addNewTodo">
    <label for="">New Todo</label>
    <input v-model="newTodo" name="newTodo" type="text" />
    <button>Add New Todo</button>
  </form>

  <div v-for="todo in todos" :key="todo.id">
    <h3>{{ todo.content }}</h3>
  </div>
</template>

<script>
import { ref } from "vue";
export default {
  setup() {
    const newTodo = ref("");
    const todos = ref([]);

    function addNewTodo() {
      todos.value.push({
        id: Date.now(),
        done: false,
        content: newTodo.value,
      });
      console.log(newTodo.value);
    }

    return {
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

.todo {
  cursor: pointer;
}

.done {
  text-decoration: line-through;
}
</style>
