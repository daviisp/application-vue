<template>
    <nav class="nav">
        <RouterLink to="/">Home</RouterLink>
        <RouterLink to="/search">Search</RouterLink>
    </nav>
</template>

<style scoped>
.container {
    width: 100%;
    background-color: #000;
    min-height: 60px;
    display: flex;
    align-items: center;
    justify-content: center;
}

.nav {
    display: flex;
    align-items: center;
    gap: 20px;
}

.nav a {
    color: #f64348;
    font-weight: 700;
    text-transform: uppercase;
    text-decoration: none;
}
</style>
