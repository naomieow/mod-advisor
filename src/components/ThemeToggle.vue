<script>
import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome';

export default {
    mounted() {
        const initUserTheme = this.getTheme() || this.getMediaPreference();
        this.setTheme(initUserTheme);
    },
    data() {
        return {
            userTheme: "light-theme",
        };
    },
    methods: {
        toggleTheme() {
            const activeTheme = localStorage.getItem("user-theme");
            if (activeTheme === "light-theme") {
                this.setTheme("dark-theme");
            }
            else {
                this.setTheme("light-theme");
            }
        },
        getTheme() {
            return localStorage.getItem("user-theme");
        },
        setTheme(theme) {
            localStorage.setItem("user-theme", theme);
            this.userTheme = theme;
            document.documentElement.className = theme;
        },
        getMediaPreference() {
            const hasDarkPreference = window.matchMedia("(prefers-color-scheme: dark)").matches;
            if (hasDarkPreference) {
                return "dark-theme";
            }
            else {
                return "light-theme";
            }
        },
    },
    components: { FontAwesomeIcon }
};
</script>

<template>
    <div>
        <input
        @change="toggleTheme"
        id="checkbox"
        type="checkbox"
        class="switch-checkbox"
        />
        <label for="checkbox" class="switch-label">
            <FontAwesomeIcon icon="fa-moon" />
            <FontAwesomeIcon icon="fa-sun" />
            <div
            class="switch-toggle"
            :class="{ 'switch-toggle-checked': userTheme === 'dark-theme' }"
            ></div>
        </label>
    </div>
</template>

<style scoped>
.switch-checkbox {
    display: none;
}

.switch-label {
    color: orange;
    align-items: center;
    background: var(--active-color);
    /* border: calc(5rem * 0.025) solid var(--text-color); */
    border-radius: 100em;
    cursor: pointer;
    display: inline-flex;
    font-size: calc(5rem * 0.3);
    position: relative;
    padding: 0.1em;
    transition: background 0.5s ease;
    justify-content: space-between;
    width: 5rem;
    height: calc(5rem * 0.35);
}

.switch-toggle {
    position: absolute;
    background-color: var(--secondary-color);
    border-radius: 50%;
    left: calc(5rem * 0.055);
    height: calc(5rem * 0.41);
    width: calc(5rem * 0.41);
    transform: translateX(-0.2em);
    transition: transform 0.3s ease, background-color 0.5s ease;
}

.switch-toggle-checked {
    transform: translateX(calc(5rem * 0.6)) !important;
}
</style>