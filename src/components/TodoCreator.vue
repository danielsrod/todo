<script setup lang="ts">
import { ref, onMounted } from 'vue';
import { uid } from 'uid';

const emit = defineEmits([
    'create-todo'
])

const todo = ref('');
const invalid = ref(false);
const inputCreateTodo = ref();
const inputTypeTodo = ref();

const createTodo = () => {
    if (todo.value.length > 0) {
        const todoObj = {
            id: uid(),
            status: false,
            text: todo.value
        }
        emit('create-todo', todoObj);
        todo.value = '';
        invalid.value = false;
        inputCreateTodo.value.focus();
        return
    }
    invalid.value = true;
}

onMounted(() => {
    inputCreateTodo.value.focus()
})
</script>

<template>
    <div class="todo__group" :class="invalid ? 'teste' : ''">
        <input :placeholder="invalid ? 'Todo should be not empty' : 'Type your todo here'" ref="inputCreateTodo"
            @keyup.enter="createTodo" class="todo__input" type="text" v-model="todo" maxlength="200">
        <button class="todo__create" @click="createTodo">Create</button>
    </div>
    <!-- <span v-show="invalid" class="invalid__todo">Todo should be not empty</span> -->
</template>


<style lang="scss" scoped>
.todo__input {
    width: 80%;
    height: 30px;
    border: none;
    padding: 10px;
    outline: none;
}

input::placeholder {
    text-align: center;
}

.teste {
    input::placeholder {
        color: red;
    }
}

.todo__create {
    width: 20%;
    height: 30px;
    border: none;
    transition: ease-in-out;
    cursor: pointer;
    color: white;
    border-left: 1px solid rgba(128, 128, 128, 0.603);
    background-color: green;
}

.todo__create:hover {
    opacity: 0.5;
}

.todo__create:active {
    opacity: 0.1;
}

.todo__group {
    border: 1px solid rgba(128, 128, 128, 0.603);
    width: 75%;
}

span {
    margin-top: 20px;
}

.invalid__todo {
    color: red;
}
</style>