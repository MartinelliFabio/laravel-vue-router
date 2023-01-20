<template>
    <div class="card h-100" style="width: 18rem;">
        <img v-if="project.cover_image" :src="`${store.imagBasePath}${project.cover_image}`" class="card-img-top" :alt="project.name_proj">
        <img v-else src="https://picsum.photos/1920/1080?random=1" class="card-img-top" :alt="project.name_proj">
        <div class="card-body">
            <h5 class="text-capitalize card-title">{{ project.name_proj }}</h5>
            <p class="card-text">{{ project.description }}</p>
            <router-link class="btn btn-primary" :to="{ name: 'single-project', params: { slug: project.slug } }">
                Vedi il project
            </router-link>
        </div>
    </div>
</template>

<script>
import { store } from '../store';
    export default {
        name: 'CardComponent',
        props: ['project']
    }
</script>

<style lang="scss" scoped>

</style>