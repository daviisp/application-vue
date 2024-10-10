<script setup>
import { ref } from "vue"

defineProps(["onSubmit"])

const searchInput = ref("")
</script>

<template>
    <form
        @submit.prevent="onSubmit(searchInput)"
        class="content flex align-center gap-3 media-screen"
    >
        <input type="text" v-model="searchInput" placeholder="Digite o usuário" />
        <button>Carregar Usuário</button>
    </form>
</template>

<style scoped>
.content {
    padding: 30px 0;
}
.flex {
    display: flex;
}

.align-center {
    align-items: center;
}

.gap-3 {
    gap: 15px;
}

button {
    background-color: #f64348;
    color: #fff;
    border-radius: 8px;
    padding: 15px 10px;
    border: none;
    text-transform: uppercase;
    font-weight: 700;
    color: #121212;
    min-width: 200px;
}

input {
    padding: 10px;
    border-radius: 5px;
    background-color: #1d1a1d;
    border-color: #f64348;
    color: #fff;
    width: 250px;
}

@media screen and (max-width: 700px) {
    .content {
        font-size: 14px;
    }

    button {
        width: 90px;
        padding: 10px 5px;
        font-size: 12px;
    }

    input {
        width: 200px;
    }
}

@media screen and (max-width: 430px) {
    .media-screen {
        flex-direction: column;
    }
}
</style>
