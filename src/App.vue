<script setup lang="ts">
import {ref,reactive,computed, defineComponent} from 'vue'

interface Todo {
  text: string;
  done: boolean;
}
const todos = ref<Todo[]>([
]);

let input = reactive<Todo>({
  text: '',
  done: false
});
let todoNum = computed(() => {
  return todos.value.length;
});
const AddTodo = () => {
  if(input.text == ''){
    alert('Please enter a todo');
    return;
  }
  todos.value.push(input);
  input = reactive<Todo>({
    text: '',
    done: false
  });
};

const DeleteTodo = () => {
  todos.value.pop();
};

</script>

<template>
<h1> My Todo App</h1>
<input type="text" v-model="input.text"/><button @click="AddTodo">Add</button><button @click="DeleteTodo">Delete</button>
<p v-if="todoNum == 0">No todos</p>
<ul v-else>
  <li v-for = "todo in todos"><input type ="checkbox" /><span>{{ todo.text }}</span></li>
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