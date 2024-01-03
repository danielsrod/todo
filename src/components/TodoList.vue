<script setup lang="ts">
import { ref } from 'vue';
import { Icon } from '@iconify/vue';

interface ITodoObj {
    id: string;
    status: boolean;
    text: string
}

defineProps<{
    props: ITodoObj
}>()

const isEditing = ref(false);
const currentTodoText = ref('');

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

// :contentEditable="false"

</script>

<template>
    <div class="list__todo">
        <p class="todo__text" :v-bind="currentTodoText" :class="props.status ? 'todo__text_done' : ''">{{ props.text }}</p>
        <div class="todo__actions">
            <div class="wrap__icons">
                <div class="wrap__icon">
                    <span @click="toggleStatus(props.id)" :class="props.status ? 'todo__done' : 'todo__pending'">
                    </span>
                </div>
                <div class="wrap__icon">
                    <span>
                        <Icon class="edit" icon="carbon:edit" />
                    </span>
                </div>
                <div class="wrap__icon">
                    <span @click="deleteTodo(props.id)">
                        <Icon class="trash" icon="ph:trash" />
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
    margin-bottom: 20px;
    margin-top: 20px;
    width: 75%;
    border-radius: 10px;
    background: #e0e0e0;
    box-shadow: 11px 11px 21px #cacaca,
        -11px -11px 21px #f6f6f6;

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
    background-color: rgb(128, 0, 0);
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
</style>