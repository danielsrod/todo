<script setup lang="ts">

import { RouterLink } from 'vue-router'

</script>

<template>
    <header>
        <nav>
            <img src="../assets/logo.png" alt="logo tesla">
            <p>Daniel TODO</p>
        </nav>
        <ul>
            <RouterLink class="router__link" to="/">Home</RouterLink>
            <RouterLink class="router__link" to="/about">About</RouterLink>
        </ul>
    </header>
</template>

<style lang="scss" scoped>
header {
    background-color: rgba(222, 222, 222, 0.500);
    font-size: 22px;
    font-family: Poppins;
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 15px;
}

ul {
    display: flex;
    flex-direction: row;
    justify-content: space-around;
    width: 200px;
}

nav {
    display: flex;
    flex-direction: column;
    align-items: center;

    img {
        width: 50px;
    }
}

.router__link {
    padding: 10px;
    text-decoration: none;
    color: black;
    border-radius: 5%;
    border-left: 1px solid rgb(200, 0, 0);
    border-width: 5px;
    transition: 0.3s ease-in-out;
}

.router__link:hover {
    opacity: 0.5;
}

.router__link:active {
    opacity: 0.1;
}
</style>