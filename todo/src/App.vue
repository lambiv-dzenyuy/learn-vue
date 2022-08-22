<script setup>
import { reactive, ref, watch } from "vue";
import TodoList from "./components/TodoList.vue";
import TodoForm from "./components/TodoForm.vue";

const todos = ref([
  {
    name: "Create first vue app",
    description: "Create a to-do app with react",
  },
  {
    name: "Refactor todo app",
    description: "refactoring with composition api",
  },
  {
    name: "Rest",
    description: "Rest while watching some episodes of the community",
  },
]);
watch(todos.value, (currentValue) => {
  if (currentValue.length === 0) {
    isToEdith.value = false;
    todoToEdith.value = {};
  }
});
const todoToEdith = reactive({
  index: null,
  data: {
    name: "",
    description: "",
  },
});

const isToEdith = ref(false);

const addNewTodo = () => {
  todos.value.push(todoToEdith.data);
  todoToEdith.data = {};
};
const deleteTodo = (index) => {
  todos.value.splice(index, 1);
  const isTodoToEdithDeleted = !todos.value[index.value];
  if (isTodoToEdithDeleted) {
    isToEdith.value = false;
    todoToEdith.data = {};
  }
};
const edithTodo = (index) => {
  isToEdith.value = true;
  todoToEdith.index = index;
  todoToEdith.data = todos.value[todoToEdith.index];
};
const edith = () => {
  todos.value[todoToEdith.index] = todoToEdith.data;
  isToEdith.value = false;
  todoToEdith.data = {};
};
</script>
<template>
  <div class="card container" v-cloak>
    <h1 class="text-center">Todo List</h1>

    <TodoList :todos="todos" :edithTodo="edithTodo" :deleteTodo="deleteTodo" />

    <br />
    <div class="card container" style="width: 50rem; background-color: aliceblue">
      <TodoForm
        v-if="!isToEdith"
        :todoToEdith="todoToEdith.data"
        :comfirmEdthTodoOrAddToTodos="addNewTodo"
        @switchForm="isToEdith = false"
        title="Add New todo"
      >
        Add to todos
      </TodoForm>
      <TodoForm
        v-else
        :todoToEdith="todoToEdith.data"
        :comfirmEdthTodoOrAddToTodos="edith"
      >
        comfirm change
      </TodoForm>
    </div>
  </div>
</template>

<style>
#app {
  border: 2px solid #4d4d38;
  background-color: rgb(188, 219, 226);
  min-height: 100vh;
}

[v-cloak] {
  display: none;
}
</style>
