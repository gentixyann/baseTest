<template>
    <div class="container">
        <PageNotFound />
        <NuxtLink to="/">
          Home page
        </NuxtLink>
    </div>
</template>

<script>
const PageNotFound = () => import('../components/PageNotFound.vue');
    export default {
        components: {
            PageNotFound
        }
    }
</script>

<style scoped>
    .container {
        padding: 5rem 0;
        display: flex;
        align-items: center;
        justify-content: center;
        height: 70vh;
    }
</style>
