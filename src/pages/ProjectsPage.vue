<template>
    <section>
        <h1>Lista dei Projects</h1>
        <div class="row mb-5">
            <div class="col-12 col-md-4 g-5" v-for="(project, index) in projects" :key="index">
                <CardComponent :project="project" />
            </div> 
        </div>
        <nav aria-label="Page navigation example">
            <ul class="pagination">
                <li class="page-item"><a class="page-link" href="#">Previous</a></li>
                <li class="page-item" v-for="n in lastPage"><a class="page-link" @click="getProject(n)">{{ n }}</a></li>
            </ul>
        </nav>
    </section>
</template>

<script>
import axios from 'axios';
import { store } from '../store';
import CardComponent from '../components/CardComponent.vue';
export default {
    name: "ProjectsPage",
    components: {
        CardComponent
    },
    data() {
        return {
            store,
            projects: [],
            currentPage: 1,
            lastPage: null,
            total: 0,
        };
    },
    methods: {
        getProject(pagenum) {
            axios.get(`${this.store.apiBaseUrl}/projects`, {
                params: {
                    page: pagenum
                }
            }).then((response) => {
                //console.log(response.data.results);
                this.projects = response.data.results;
                this.currentPage = response.data.results.current_page;
                this.lastPage = response.data.results.last_page;
                this.total = response.data.results.total;
            });
        },
    },
    mounted() {
        this.getProject(1);
    },
}
</script>

<style lang="scss" scoped>

</style>