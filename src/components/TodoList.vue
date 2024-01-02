<script setup lang="ts">

interface ITodoObj {
    status: boolean;
    text: string
}

defineProps<{
    props: ITodoObj
}>()

</script>

<template>
    <div class="list__todo">
        <p>{{ props.text }}</p>
        <span>{{ props.status }}</span>
    </div>
</template>


<style lang="scss" scoped>
.list__todo {
    display: flex;
    flex-direction: column;
    padding: 10px;
    margin-bottom: 20px;
    margin-top: 20px;
    width: 310px;
    border-radius: 10px;
    background: #e0e0e0;
    box-shadow: 11px 11px 21px #cacaca,
        -11px -11px 21px #f6f6f6;
}

.list__todo>span {
    text-align: end;
}
</style>