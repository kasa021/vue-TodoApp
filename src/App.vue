<script setup lang="ts">
import {ref,reactive,computed, defineComponent} from 'vue'

const data = () =>({

})

</script>

<template>
<h1> My Todo App</h1>
<input type="text"/><button>Add</button><button>Delete</button>
<ul>
  <li>
    <input type="checkbox"  checked/><span class="todo-done"
    >Learn Vue</span>
  </li>
  <li><intput type ="checkbox"/><span> buy milk</span></li>
  <li><intput type ="checkbox"/><span> buy eggs</span></li>
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