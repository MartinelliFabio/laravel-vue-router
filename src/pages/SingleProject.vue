<template>
    <section v-if="project">
        <h1>{{ project.name_proj }}</h1>
        <img v-if="project.cover_image" :src="`${store.imagBasePath}${project.cover_image}`" class="card-img-top" :alt="project.name_proj">
        <img v-else src="https://picsum.photos/id/20/1920/1080" class="card-img-top" :alt="project.name_proj">
        <p>{{ project.name }}</p>
        <div v-if="project.type">
            <h5>Category: {{ project.category.worflow }}</h5>
        </div>
        <div v-if="project.language && project.language.length > 0">
            <h5>Tags</h5>
            <div>
                <span v-for="(language, index) in project.languages" :key="index" class="badge text-bg-info">{{ language.name }}</span>
            </div>
        </div>
    </section>
    <section v-else>Loading...</section>
</template>

<script>
import axios from 'axios';
import { store } from '../store';
export default {
    name: 'SinglePost',
    data() {
        return {
            store,
            project: null,
        }
    },
    methods: {
        getProject() {
            console.log(this.$route);
            axios.get(`${this.store.apiBaseUrl}/projects/${this.$route.params.slug}`).then((response) => {
                //console.log(response.data.results);
                if (response.data.success) {
                    //console.log(response.data.results);
                    this.project = response.data.results;
                } else {
                    //console.log(this.$router);
                    this.$router.push({ name: 'not-found' });
                }

            });

        }
    },
    mounted() {
        this.getProject();
    }

}
</script>

<style lang="scss" scoped>

</style>