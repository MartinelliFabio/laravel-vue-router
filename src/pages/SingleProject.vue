<template>
    <section v-if="project">
        <h1 class="text-capitalize">{{ project.name_proj }}</h1>
        <div class="img-box">
            <img v-if="project.cover_image" :src="`${store.imagBasePath}${project.cover_image}`" class="card-img-top single-img" :alt="project.name_proj">
            <img v-else src="https://picsum.photos/1200/600?random=1" class="card-img-top" :alt="project.name_proj">
        </div>
        <!-- <div><strong>Workflow:</strong> {{ project.type.workflow }}</div> -->
        <div><strong>Framework:</strong> {{ project.dev_framework }}</div>
        <div><strong>Livello Difficoltà:</strong> {{ project.lvl_dif }}</div>
        <div><strong>Team:</strong> {{ project.team }}</div>
        <div><strong>Link Github:</strong> {{ project.link_git }}</div>
        <div><strong>Descrizione:</strong> {{ project.description }}</div>
    </section>
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
    
    .single-img {
        width: auto;
        height: 600px;
        background-size: contain;
    }

</style>