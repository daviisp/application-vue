<script setup>
import { reactive, computed, ref } from "vue"
import UserInfo from "./UserInfo.vue"
import Repository from "./Repository.vue"
import Form from "./Form.vue"

const state = reactive({
    login: "",
    name: "",
    bio: "",
    company: "",
    avatar_url: "",
    userNotFound: false,
    repos: [],
})

async function fetchGithubUser(searchInputValue) {
    const res = await fetch(`https://api.github.com/users/${searchInputValue}`)

    if (res.status !== 200) {
        state.userNotFound = true

        state.login = ""
        state.name = ""
        state.bio = ""
        state.company = ""
        state.avatar_url = ""

        return
    }

    state.userNotFound = false

    const { login, name, bio, company, avatar_url } = await res.json()

    state.login = login
    state.name = name
    state.bio = bio
    state.company = company
    state.avatar_url = avatar_url

    await fetchReposGithubUser()
}

async function fetchReposGithubUser() {
    const res = await fetch(`https://api.github.com/users/${state.login}/repos`)

    state.repos = await res.json()
}

const countReposMessage = computed(() => {
    return state.repos.length > 0
        ? `${state.name} tem ${state.repos.length} repositórios públicos`
        : `${state.name} não tem nenhum repositório público`
})
</script>

<template>
    <h1>GitHub User Data</h1>
    <p class="content">Digite o nome do usuário do GitHub que você deseja pesquisar</p>
    <Form :onSubmit="fetchGithubUser" />
    <p v-if="state.userNotFound" class="user-not-found">Usuário não encontrado</p>
    <div v-if="state.login && state.name" class="flex flex-col align-center gap-3">
        <UserInfo
            :name="state.name"
            :avatar_url="state.avatar_url"
            :bio="state.bio"
            :company="state.company"
            :login="state.login"
        />
    </div>
    <h1 v-if="state.login && state.name">{{ countReposMessage }}</h1>
    <div class="repos-container" v-if="state.login && state.repos.length > 0">
        <div v-for="repository in state.repos" :key="repository.id" class="repo-content">
            <Repository
                :full_name="repository.full_name"
                :description="repository.description"
                :html_url="repository.html_url"
            />
        </div>
    </div>
</template>

<style>
h1 {
    color: #f64348;
    text-align: center;
    display: block;
    padding-top: 30px;
}

.user-not-found {
    color: red;
}

.content {
    padding: 30px 0;
}

.flex {
    display: flex;
}

.flex-col {
    flex-direction: column;
}

.align-center {
    align-items: center;
}

.gap-3 {
    gap: 15px;
}

.content {
    color: #ffffffc9;
    text-align: center;
}

.repos-container {
    padding-top: 20px;
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 10px;
    position: relative;
}

.repo-content {
    background-color: #000;
    color: #fff;
    padding: 10px;
    border-radius: 15px;
    max-width: 300px;
}

.justify-end {
    justify-content: end;
    margin-top: auto;
}

input:focus {
    outline: none;
}

input::placeholder {
    color: #fafafa;
}

@media screen and (max-width: 700px) {
    h1 {
        font-size: 23px;
    }

    .content {
        font-size: 14px;
    }

    .repos-container {
        display: flex;
        flex-direction: column;
        gap: 8px;
    }
}

@media screen and (max-width: 430px) {
    .media-screen {
        flex-direction: column;
    }
}
</style>
