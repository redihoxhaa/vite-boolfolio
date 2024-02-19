<script>
// IMPORTS

import ProjectCard from '../components/ProjectCard.vue';
import PageScroller from '../components/PageScroller.vue';
import axios from 'axios';
import PostSearch from '../components/PostSearch.vue';
import store from '../store';

// /IMPORTS

export default {
    components: { ProjectCard, PageScroller, PostSearch },
    data() {
        return {
            store,
            projects: [],
            errors: [],
        }
    },
    methods: {
        getProjects() {
            this.errors = '';
            axios.get(this.store.baseURL + this.store.URIs.projects + this.store.params.page.prefix + this.store.params.page.page_number, {
                params: {
                    key: this.store.searchKey,
                }
            }).then(response => {
                console.log(response);
                this.projects = response.data.result.data;
                this.store.params.page.max_pages = response.data.result.last_page;
            }).catch(
                error => {
                    console.log(error);
                    this.projects = [];
                    this.errors = error.response.data.message;
                }
            )
        },
        prevPage() {
            if (this.store.params.page.page_number > 1) {
                this.store.params.page.page_number--;
                this.$router.push({ name: 'projects', query: { page: this.store.params.page.page_number, key: this.store.searchKey } });
                this.getProjects();
            }
        },

        nextPage() {
            if (this.store.params.page.page_number < this.store.params.page.max_pages) {
                this.store.params.page.page_number++;
                this.$router.push({ name: 'projects', query: { page: this.store.params.page.page_number, key: this.store.searchKey } });
                this.getProjects();
            }
        }
    },
    created() {
        this.store.params.page.page_number = this.$route.query?.page ?? 1;
        this.store.searchKey = this.$route.query.key ?? null;
        // this.$watch(
        //     () => this.$route.params,
        //     (toParams, previousParams) => {
        //         this.params.page.page_number = this.$route.query?.page ?? 1;
        //         this.getProjects();
        //     }),
        this.getProjects();
    },
}
</script>

<template>
    <h3 class="pt-5 text-center">My projects</h3>
    <PostSearch @searchProject="getProjects()" />

    <div v-if="errors.length">{{ errors }}</div>
    <ul class="row g-5">
        <li class="col-12 col-md-6 col-lg-4 d-flex" v-for="project in projects">
            <ProjectCard :project="project" />
        </li>
    </ul>
    <PageScroller @prevPage="prevPage()" @nextPage="nextPage()" />
</template>

<style lang="scss" scoped>
// USES

@use '../assets/scss/partials/reset' as *;

// /USES
</style>
