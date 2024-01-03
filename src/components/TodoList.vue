<script setup lang="ts">
import { ref } from 'vue';
import { Icon } from '@iconify/vue';

import { ITodoObj, IEditTodoObj } from '../interfaces/index.ts'

defineProps<{
    props: ITodoObj
}>()

const isEditing = ref(false);
const currentTodoText = ref();

const emits = defineEmits([
    'toggle-status',
    'delete-todo',
    'edit-todo'
])

const toggleStatus = (todoId: string) => {
    emits('toggle-status', todoId);
}

const deleteTodo = (todoId: string) => {
    emits('delete-todo', todoId)
}

const confirmEditTodo = (todoId: string) => {
    const objEditTodo: IEditTodoObj = {
        todoId: todoId,
        todoText: currentTodoText.value.innerText
    }
    emits('edit-todo', objEditTodo)
    isEditing.value = false;
}

const cancelEditTodo = () => {
    isEditing.value = false;
}

</script>

<template>
    <div class="list__todo">
        <p v-if="!isEditing" class="todo__text" :v-bind="currentTodoText" :class="props.status ? 'todo__text_done' : ''">{{
            props.text }}</p>
        <p v-else ref="currentTodoText" :contentEditable="true" @keyup.enter="confirmEditTodo(props.id)">{{ props.text }}
        </p>
        <div class="todo__actions">
            <div v-if="!isEditing" class="wrap__icons">
                <div class="wrap__icon">
                    <span @click="toggleStatus(props.id)" :class="props.status ? 'todo__done' : 'todo__pending'">
                    </span>
                </div>
                <div class="wrap__icon">
                    <span @click="isEditing = !isEditing">
                        <Icon class="edit" icon="carbon:edit" />
                    </span>
                </div>
                <div class="wrap__icon">
                    <span @click="deleteTodo(props.id)">
                        <Icon class="trash" icon="ph:trash" />
                    </span>
                </div>
            </div>
            <div v-else class="wrap__icons__editing">
                <div class="wrap__icon">
                    <span @click="confirmEditTodo(props.id)">
                        <Icon class="edit" icon="line-md:confirm" />
                    </span>
                </div>
                <div class="wrap__icon">
                    <span @click="cancelEditTodo">
                        <Icon class="trash" icon="fluent-mdl2:cancel" />
                    </span>
                </div>
            </div>
        </div>
    </div>
</template>


<style lang="scss" scoped>
.todo__text {
    word-wrap: break-word;
}

.list__todo {
    display: flex;
    flex-direction: column;
    padding: 10px;
    font-family: Poppins, sans-serif;
    font-weight: 400;
    margin: 4px 4px 20px 4px;
    border-radius: 7px;
    background: #e0e0e0;

    div {
        display: flex;
    }
}

.todo__done {
    width: 25px;
    height: 25px;
    background-color: green;
    border-radius: 100%;
}

.todo__pending {
    width: 25px;
    height: 25px;
    background-color: rgb(200, 0, 0);
    border-radius: 100%;
}

.todo__text_done {
    text-decoration: line-through;
    font-style: italic;
    color: #676767;
}

span {
    cursor: pointer;
    transition: 0.3 ease-in-out;
}

span:hover {
    opacity: 0.5;
}

span:active {
    opacity: 0.1;
}

.trash {
    width: 100%;
    height: 100%;
}

.edit {
    width: 100%;
    height: 100%;
}

.todo__actions {
    height: 25px;
    display: flex;
    justify-content: end;
}

.wrap__icon {
    width: 25px;
    height: 25px;
}

.wrap__icons {
    display: flex;
    justify-content: space-between;
    width: 120px;
}

.wrap__icons__editing {
    display: flex;
    justify-content: space-between;
    width: 80px;
}
</style>