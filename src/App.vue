<template>
  <div class="container">
    <div class="row justify-content-center">
      <div class="col-md-8">
        <div class="todolist">
          <h1>Vue 3 To-Do List</h1>

          <form @submit.prevent="addNewTodo">
            <label for="">New Todo</label>
            <input
              class="form-control add-todo"
              v-model="newTodo"
              name="newTodo"
              type="text"
            />
            <!-- <button>Add New Todo</button> -->
          </form>
          <div class="form-actions">
            <button class="btn btn-danger" @click="removeAll">
              Remove All
            </button>
            <button class="btn btn-success" @click="markAllDone">
              Mark All Done
            </button>
          </div>

          <hr v-if="todos.length > 0" />

          <ul class="list-unstyled">
            <li
              class="ui-state-default"
              v-for="(todo, index) in todos"
              :key="todo.id"
              :class="{ done: todo.done }"
              @click="toggleDone(todo)"
            >
              {{ todo.content }} <span class="flex-fill"></span>
              <button
                class="remove-item btn btn-default btn-xs pull-right"
                @click="removeTodo(index)"
              >
                <i class="far fa-trash-alt"></i>
              </button>
            </li>
          </ul>
        </div>
      </div>
    </div>
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
      newTodo.value = "";
    }

    function toggleDone(todo) {
      todo.done = !todo.done;
    }

    function removeTodo(index) {
      todos.value.splice(index, 1);
    }

    function markAllDone() {
      todos.value.forEach((todo) => (todo.done = true));
    }

    function removeAll() {
      todos.value = [];
    }

    return {
      todos,
      newTodo,
      addNewTodo,
      toggleDone,
      removeTodo,
      markAllDone,
      removeAll,
    };
  },
};
</script>

<style>
.form-actions {
  margin-top: 10px;
  text-align: right;
}

.form-actions > *:not(:last-child) {
  margin-right: 5px;
}

.todolist {
  background-color: #fff;
  padding: 20px 20px 10px 20px;
  margin-top: 30px;
}
.todolist h1 {
  margin: 0;
  padding-bottom: 20px;
  text-align: center;
}

.form-control {
  border-radius: 0;
}

li.ui-state-default {
  background: #fff;
  border: none;
  display: flex;
  align-items: center;
  border-bottom: 1px solid #ddd;
  cursor: pointer;
}

li.ui-state-default:last-child {
  border-bottom: none;
}

.done {
  text-decoration: line-through;
}
</style>
