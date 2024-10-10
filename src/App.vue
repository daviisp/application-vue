<script setup>
import Nav from "./components/Nav.vue"
</script>

<template>
    <Nav />
    <div class="border" />
    <RouterView></RouterView>
</template>

<style>
.border {
    border: 1px solid #fff;
    width: 100vw;
    margin: 20px 0;
}

#app {
    display: flex;
    flex-direction: column;
    align-items: center;
    height: 100vh;
    padding: 40px 0;
}
</style>
