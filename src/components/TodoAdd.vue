<template>
    <input type="text" v-model="inputText" />
    <MyButton @click="emit('AddTodo')">Add</MyButton>
    <MyButton @click="emit('DeleteTodo')">Delete</MyButton>
</template>

<script setup lang="ts">
import { computed } from 'vue';
import MyButton from './MyButton.vue';

interface Emit {
    (e: 'AddTodo'): void;
    (e: 'DeleteTodo'): void;
    (e: 'update:text', newtext: string): void;
}
const emit = defineEmits<Emit>();

interface Props {
    text: string;
}
const props = defineProps<Props>();

const inputText = computed({
    get: () => props.text,
    set: (newText: string) => emit('update:text', newText)
});
</script>