<script>
import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome';
import axios from 'axios';

export default {
    name: "ModVue",
    props: {
        slug: { type: String, required: true }
    },
    setup() {
    },
    data() {
        return {
            info: null,
            author: null
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
    <template v-for="(item, index) in info">
        <div v-if="index == 'data'">
            <a :href="'mods/'+item.slug" class="mod-container">
                <img class="mod-icon" :src="item.icon_url" />
                <div class="mod-info">
                    <div class="top">
                        <h2>{{ item.title }}</h2>
                        <p>by {{ author }}</p>
                    </div>
                    <p class="description">{{ item.description }}</p>
                </div>
                <div class="reviews-info">
                    <div class="count">
                        <FontAwesomeIcon icon="fa-book" />
                        <p>x Reviews</p>
                    </div>
                </div>
            </a>
        </div>
    </template>
</template>

<style scoped>
.reviews-info {
    display: flex;
    float: right;
}
.reviews-info .count{
    display: flex;
    flex-direction: row;
    align-items: center;
}
.top {
    align-items: baseline;
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
    flex-shrink: 0;
}

.mod-icon {
    transition: 0.1s ease;
    height: 6rem;
    border-radius: 1.25rem;
}

.mod-container {
    display: flex;

    background-color: var(--secondary-color);

    border-radius: 1.25rem;
    box-shadow: rgba(0, 0, 0, 0.24) 0px 3px 8px;

    margin: 1rem;
    padding: 1rem;

    color: var(--text-color);
    text-decoration: none;
}

.mod-container:hover {
    background-color: var(--active-color);
}

.mod-container:hover .mod-icon {
    transition: 0.2s ease;
    height: 9rem;
    
}

    
.mod-container a {
    width: 100%;
    height: 100%;
    position: relative;
    left: 0;
    top: 0;
}

.mod-info {
    margin-left: 0.5rem;
}
.mod-info h2{
    margin: 0.5rem;
    margin-bottom: 0.25rem
}
.description {
    margin: 0;
    margin-left: 1rem;
    max-width: 75%;
}
</style>