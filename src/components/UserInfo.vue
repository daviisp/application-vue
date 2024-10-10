<script setup>
defineProps(["login", "name", "bio", "company", "avatar_url"])
</script>

<template>
    <img :src="avatar_url" />
    <strong class="login">@{{ login }}</strong>
    <h2 class="name">{{ name }}</h2>
    <h3 class="company">{{ company }}</h3>
    <span class="bio">{{ bio }}</span>
</template>

<style scoped>
strong {
    color: #fff;
}
h2 {
    color: #f64348;
    text-align: center;
    display: block;
}

h3,
span {
    color: #fafafa;
}

img {
    width: 200px;
    height: 200px;
    border-radius: 100%;
}
</style>
