<template>
  <div class="card container" style="width: 50rem">
    <ul class="list-group">
      <li
        class="list-group-item"
        style="height: 6em"
        v-for="(todo, i) in props.todos"
        :key="i"
      >
        <span>
          <em><b>Title : </b></em> {{ todo.name }}</span
        ><br />
        <span>
          <em><b>Description : </b></em> {{ todo.description }}</span
        >
        <button class="badge btn btn-outline-danger" @click="deleteTodo(i)">
          remove
        </button>
        <button class="badge btn btn-outline-danger" @click="edithTodo(i)">edith</button>
      </li>
    </ul>
  </div>
</template>
<script setup>
const props = defineProps({
  todos: Array,
  edithTodo: Function,
  deleteTodo: Function,
});
</script>
