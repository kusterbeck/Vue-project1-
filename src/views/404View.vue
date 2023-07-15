<template>
    <div class="error container d-flex align-items-center justify-content-center">
        <h1 class="text-light">404 Not Found</h1>
    </div>
</template>

<script>
export default {
    name: '404View',
    
}
</script>

<style scoped>
.error {
    background-image: linear-gradient(137deg in oklab, oklch(100% 0.09 360) 0%, oklch(37% 0.38 310) 100%);
    height: 40rem;
}
h1 {
    font-size: 8rem;
}
</style>