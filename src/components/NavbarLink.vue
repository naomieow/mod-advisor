<script>
    import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome';
    import { computed } from 'vue';
    import { RouterLink, useRoute } from 'vue-router';

    export default {
    props: {
        to: { type: String, required: true },
        icon: { type: String, required: true }
    },
    setup(props) {
        const route = useRoute();
        const isActive = computed(() => route.path === props.to);
        return { isActive };
    },
    components: { RouterLink, FontAwesomeIcon }
};
</script>

<template>
    <RouterLink :to="to" class="link" :class="{ active: isActive }">
        <h1>
            <FontAwesomeIcon class="icon" :icon="icon" />
            <slot />
        </h1>
    </RouterLink>
</template>

<style>
.link {
    font-size: 12px;
    margin: 0.3em;
    /* border: 0.2em solid; */
    border-radius: 100em;
    color: var(--text-color);
    text-decoration: none;
}

.link h1 {
    margin: 0.3em;
}

.link:hover {
    background-color: var(--active-color);
    box-shadow: rgba(0, 0, 0, 0.24) 0px 1px 8px;
}

.link .icon {
    margin-right: 0.3em;
    margin-left: 0.15em;
}
</style>