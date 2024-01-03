<script setup lang="ts">
import { ref, onMounted } from 'vue';

import TodoCreator from '../components/TodoCreator.vue'
import TodoList from '../components/TodoList.vue'

interface ITodoObj {
    id: string;
    status: boolean;
    text: string;
}

const todos = ref<ITodoObj[]>([]);

// TODO: load onmouted todos in localstorage
onMounted(() => {
    todos.value = JSON.parse(localStorage.getItem('todoList') || '[]');
})

const createTodo = (todo: ITodoObj): void => {
    todos.value.unshift(todo)
    localStorage.setItem('todoList', JSON.stringify(todos.value));
}

const toggleStatus = (todoId: string): void => {
    const todoIndex = todos.value.findIndex(todo => {
        return todo.id === todoId
    })
    todos.value[todoIndex].status = !todos.value[todoIndex].status;
    localStorage.setItem('todoList', JSON.stringify(todos.value));
}

const deleteTodo = (todoId: string): void => {
    const todoIndex = todos.value.findIndex(todo => {
        return todo.id === todoId
    })
    todos.value.splice(todoIndex, 1)
    localStorage.setItem('todoList', JSON.stringify(todos.value));
}
</script>

<template>
    <main>
        <h1>Create Todo</h1>
        <TodoCreator class="todo__creator" @create-todo="createTodo" />
        <TodoList @toggle-status="toggleStatus" @delete-todo="deleteTodo" v-if="todos.length > 0" class="todo__list"
            v-for="todo in todos" :props="todo" />
        <span class="todos__list__empty" v-else>You don't have any todo. Create one</span>
    </main>
</template>

<style lang="scss" scoped>
main {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    padding: 25px;
    font-family: Poppins;
}

.todo__creator {
    margin-bottom: 20px;
}

.todo__list {
    display: flex;
    justify-content: space-between;
}

.todos__list__empty {
    margin-top: 20px;
    font-size: 20px;
}
</style>