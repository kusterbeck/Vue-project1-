<template>
    <div>
        <nav class="navbar navbar-dark bg-dark">
            <div class="container-fluid">
                <a class="navbar-brand" href="#">
                    <router-link to="/" class="text-light navbar-text"> Games opinion </router-link>
                </a>
            </div>
        </nav>
    </div>
</template>

<script>
export default {
    name: 'MyNavbar',
}
</script>

<style scoped>
.navbar-text {
    text-decoration: none;
}
</style>