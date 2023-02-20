<script setup lang="ts">
import { ref, reactive, computed, onMounted, onBeforeUnmount, watch } from 'vue'
import TodoAdd from './components/TodoAdd.vue'


interface Todo {
  text: string;
  isDone: boolean;
}
const todos = ref<Todo[]>([
]);

let input = reactive<Todo>({
  text: '',
  isDone: false
});
let todoNum = computed(() => {
  return todos.value.length;
});
const AddTodo = () => {
  if (input.text == '') {
    alert('Please enter a todo');
    return;
  }
  todos.value.push(input);
  input = reactive<Todo>({
    text: '',
    isDone: false
  });
};

const DeleteTodo = () => {
  todos.value = todos.value.filter(todo => !todo.isDone);
};

onMounted(() => {
  const todosString = localStorage.getItem("todos");
  if (todosString) {
    todos.value = JSON.parse(todosString);
  }
});

const setToLocalStorage = () => {
  localStorage.setItem("todos", JSON.stringify(todos.value));
};

watch(todos, setToLocalStorage, { deep: true });


</script>

<template>
  <h1> My Todo App</h1>
  <TodoAdd @add-todo="AddTodo" @delete-todo="DeleteTodo" v-model:text="input.text" />
  <p v-if="todoNum == 0">No todos</p>
  <ul v-else>
    <li v-for="todo in todos"><input type="checkbox" @input="setToLocalStorage" v-model="todo.isDone" /><span
        :class="{ 'todo-done': todo.isDone }">{{
          todo.text }}</span></li>
  </ul>
</template>

<style>
body {
  background-color: #eee;
}

.todo-done {
  text-decoration: line-through;
}
</style>