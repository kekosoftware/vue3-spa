<template>
    <nav>
        <RouterLink to="/home">Home</RouterLink>
        <RouterLink to="/gifs">Gifs</RouterLink>
        <RouterLink to="/about">About</RouterLink>
    </nav>
    <RouterView />
</template>

<script>
import { RouterView, RouterLink } from 'vue-router';

export default {
    components: {
        RouterView,
    }
}
</script>