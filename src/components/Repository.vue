<script setup>
defineProps(["full_name", "description", "html_url"])
</script>

<template>
    <div class="container">
        <p class="name">{{ full_name }}</p>
        <p v-if="description" class="description">
            {{ description }}
        </p>
        <div class="flex justify-end see-project">
            <a :href="html_url" target="_blank">Ver projeto</a>
        </div>
    </div>
</template>

<style scoped>
.name {
    color: #f64348;
    font-weight: 700;
}

.description {
    font-size: 14px;
}
.flex {
    display: flex;
}

.justify-end {
    justify-content: end;
    margin-top: auto;
}

.container {
    position: relative;
    min-height: 150px;
    padding: 5px;
}

.see-project {
    position: absolute;
    right: 0;
    bottom: 0;
}

.see-project a {
    text-decoration: none;
    color: #fafafa;
    cursor: pointer;
    font-size: 14px;
}

@media screen and (max-width: 650px) {
    .name,
    .description,
    .see-project {
        font-size: 12px;
    }
}
</style>
