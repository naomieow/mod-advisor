<script>
import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome';
import axios from 'axios';

export default {
    props: {},
    setup() {
    },
    data() {
        return {
            info: null,
            author: null,
            slug: this.$route.params.slug,
        };
    },
    mounted() {
        axios
            .get("https://api.modrinth.com/v2/project/" + this.slug)
            .then(response => (this.info = response));
        axios
            .get("https://api.modrinth.com/v2/project/" + this.slug + "/members")
            .then(response => (this.author = response.data[0].user.username));
    },
    components: { FontAwesomeIcon }
};
</script>

<template>
    <div class="wrapper">
        <div class="left-side">
            <div class="info-container">
                <template v-for="(item, index) in info">
                    <div v-if="index == 'data'">
                        <img class="mod-icon" :src="item.icon_url" />
                        <div class="mod-info">
                            <div class="top">
                                <h2>{{ item.title }}</h2>
                            </div>
                            <p class="description">{{ item.description }}</p>
                        </div>
                    </div>
                </template>
                <hr/>
                <div class="review-info">
                    <div class="inline"><FontAwesomeIcon icon="fa-book"/><h2>17</h2><p>reviews</p></div>
                    <div class="inline"><FontAwesomeIcon icon="fa-heart"/><h2>4.3</h2><p>hearts</p></div>
                </div>
                <hr/>
                <div class="util-buttons">
                    <button class="util-button" role="button">
                        <FontAwesomeIcon class="icon" icon="fa-font-awesome" />
                        Report
                    </button>
                    <button class="util-button" role="button">
                        <FontAwesomeIcon class="icon" icon="fa-pen-nib" />
                        Review
                    </button>
                </div>
            </div>
            <div class="info-container">
                {{ author }}
            </div>
        </div>
        <div class="info-container">
            <h1>Information</h1>
        </div>
    </div>
</template>

<style scoped>
.wrapper {
    display: grid;
    grid-template-columns: 1fr 2fr;
    gap: 1em;
}

.util-buttons {
    display: flex;
    flex-wrap: wrap;
    width: auto;
    align-items: stretch;
    gap: 1em;
}

.util-button {
    flex: 1;
    align-items: center;
    background: var(--tertiary-color);
    border: 0 solid #E2E8F0;
    box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1), 0 2px 4px -1px rgba(0, 0, 0, 0.06);
    box-sizing: border-box;
    color: var(--text-color);
    display: inline-flex;
    font-family: Inter, sans-serif;
    font-size: 1rem;
    font-weight: 700;
    height: 100%;
    justify-content: center;
    line-height: 24px;
    overflow-wrap: break-word;
    padding: 0.4em;
    text-decoration: none;
    width: auto;
    border-radius: 0.7em;
    cursor: pointer;
    user-select: none;
    -webkit-user-select: none;
    touch-action: manipulation;
}

.util-button:hover {
    background: var(--active-color);
}

.inline {
    display: inline-flex;
    align-items: baseline;
    gap: 0.3em;
}

.inline p {
    margin-top: 0;
    margin-bottom: 0;
}

.review-info {
    display: flex;
    flex-direction: column;
}

h2 {
    margin-top: 0.3em;
    margin-bottom: 0.2em;
}

.mod-icon {
    height: 9rem;
    border-radius: 1.25rem;
}

.info-container {
    background-color: var(--secondary-color);
    box-shadow: rgba(0, 0, 0, 0.24) 0px 3px 8px;

    height: auto;

    border-radius: 1.25rem;

    margin-top: 0.75em;
    padding: 1em;
}
</style>