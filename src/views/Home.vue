<script setup lang="ts">
import { ref } from 'vue';

import TodoCreator from '../components/TodoCreator.vue'
import TodoList from '../components/TodoList.vue'

interface ITodoObj {
    status: boolean;
    text: string
}

const todos = ref<ITodoObj[]>([]);

const createTodo = (todo: ITodoObj) => {
    todos.value.push(todo)
}
</script>

<template>
    <main>
        <h1>Create Todo</h1>
        <TodoCreator class="todo__creator" @create-todo="createTodo" />
        <TodoList class="todo__list" v-for="todo in todos" :props="todo" />
    </main>
</template>

<style lang="scss" scoped>
main {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    padding: 25px;
}

.todo__creator {
    margin-bottom: 20px;
}

.todo__list {
    display: flex;
    justify-content: space-between;
}
</style>