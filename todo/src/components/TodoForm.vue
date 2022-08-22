<template>
  <form>
    <h4 v-if="title">
      {{ title }}
    </h4>
    <h4 v-else>Edith : {{ todoToEdith.name }}</h4>
    <div class="form-group">
      <label for="exampleInputEmail1">Title</label>
      <input
        class="form-control"
        v-model="todoToEdith.name"
        :placeholder="todoToEdith.name"
      />
    </div>
    <div class="form-group">
      <label for="exampleInputPassword1">Description</label>
      <input
        class="form-control"
        v-model="todoToEdith.description"
        :placeholder="todoToEdith.description"
      />
    </div>
    <button
      @click.prevent="comfirmEdthTodoOrAddToTodos"
      @click="$emit('switchForm')"
      class="btn btn-primary"
    >
      <slot />
    </button>
  </form>
</template>

<script setup>
const props = defineProps({
  title: String,
  comfirmEdthTodoOrAddToTodos: Function,
  todoToEdith: {
    default: {
      name: "Enter todo title",
      description: "Enter todo description",
    },
  },
});

const emit = defineEmits(["switchForm"]);
</script>
