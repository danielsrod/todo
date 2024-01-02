<script setup lang="ts">

import { RouterLink } from 'vue-router'

</script>

<template>
    <header>
        <nav>
            <p>imagem foda</p>
            <p>Daniel TODO</p>
        </nav>
        <ul>
            <RouterLink to="/">Home</RouterLink>
            <RouterLink to="/about">About</RouterLink>
        </ul>
    </header>
</template>

<style lang="scss" scoped>
header {
    background-color: rgba(128, 128, 128, 0.473);
    font-size: 22px;
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 30px;
}

ul {
    display: flex;
    flex-direction: row;
    justify-content: space-around;
    width: 200px;
}
</style>