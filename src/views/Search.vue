<script setup>
import Main from "@/components/Main.vue"
import { ref } from "vue"

const isOpen = ref(true)
</script>

<template>
    <input type="checkbox" name="isOpen" id="isOpen" v-model="isOpen" />
    <Main v-if="isOpen" />
</template>

<style scoped></style>
