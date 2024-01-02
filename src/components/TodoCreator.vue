<script setup lang="ts">
import { ref } from 'vue';

const emit = defineEmits([
    'create-todo'
])

const todo = ref('');
const invalid = ref(false)

const createTodo = () => {
    if (todo.value.length > 0) {
        const todoObj = {
            status: false,
            text: todo.value
        }
        emit('create-todo', todoObj);
        todo.value = '';
        invalid.value = false;
        return
    }
    invalid.value = true;
}
</script>

<template>
    <div class="todo__group">
        <input class="todo__input" type="text" v-model="todo">
        <button class="todo__create" @click="createTodo">Create</button>
    </div>
    <span v-show="invalid" class="invalid__todo">Todo should be not empty</span>
</template>


<style lang="scss" scoped>
.todo__input {
    width: 250px;
    height: 30px;
    border: none;
}

.todo__create {
    width: 60px;
    height: 30px;
    border: none;
    transition: ease-in-out;
}

.todo__create:hover {
    opacity: 0.5;
}

.todo__create:active {
    opacity: 0.1;
}

.todo__group {
    border: 1px solid rgba(128, 128, 128, 0.603);
}

span {
    margin-top: 20px;
}

.invalid__todo {
    color: red;
}
</style>