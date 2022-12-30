<script setup>
import { RouterLink, RouterView } from 'vue-router';
import NavbarVue from './components/Navbar.vue';
</script>

<template>
    <NavbarVue />
    <div class="router-app">
        <RouterView />
    </div>
</template>

<style>
.router-app {
    padding-top: var(--navbar-height);
}
</style>
