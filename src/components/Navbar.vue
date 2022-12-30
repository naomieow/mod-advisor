<script>
    import NavbarLinkVue from './NavbarLink.vue';
    import { RouterLink } from 'vue-router';
import ThemeToggle from './ThemeToggle.vue';

    export default {
        name: "navbar",
        props: {},
        components: { NavbarLinkVue, ThemeToggle },
        setup() {
        }
    };
</script>

<template>
    <div class="navbar ">
        <NavbarLinkVue to="/" icon="fa-house">Modadvisor</NavbarLinkVue>
        <h1>TODO: add seach bar here</h1>
        <NavbarLinkVue to="/mods" icon="fa-code">Mods</NavbarLinkVue>
        <NavbarLinkVue to="/creators" icon="fa-users">Creators</NavbarLinkVue>
        <NavbarLinkVue to="/profile" icon="fa-user">Profile</NavbarLinkVue>
        <ThemeToggle />
    </div>
</template>

<style scoped>
.navbar {
    display: grid;
    position: fixed;
    width: 60%;
    grid-template-columns: 1fr 2fr repeat(4, auto);
    justify-content: center;
    align-items: center;

    background-color: var(--background-color);
    
    padding-top: 8px;
    padding-bottom: 5px;

    border-bottom: 1px solid;
}

.navbar h1 {
    margin: 5px;
}

.full-seperator {
    width: 100vw;
}
</style>