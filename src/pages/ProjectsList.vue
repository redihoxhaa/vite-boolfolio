<script>
// IMPORTS

import ProjectCard from '../components/ProjectCard.vue';
import PageScroller from '../components/PageScroller.vue';
import axios from 'axios';

// /IMPORTS

export default {
    props: ['projects'],
    components: { ProjectCard, PageScroller },
    emits: ['prevPage', 'nextPage'],
    data() {
        return {
            projects: [],
            baseURL: 'http://127.0.0.1:8000',
            URIs: {
                projects: '/api/projects'
            },
            params: {
                page: {
                    prefix: '?page=',
                    page_number: 1,
                    max_pages: ''
                }
            }
        }
    },
    methods: {
        getProjects() {
            axios.get(this.baseURL + this.URIs.projects + this.params.page.prefix + this.params.page.page_number).then(response => {
                this.projects = response.data.data;
                this.params.page.max_pages = response.data.last_page;
            })
        },

        prevPage() {
            if (this.params.page.page_number > 1) {
                this.params.page.page_number--;
                this.getProjects();
            }
        },

        nextPage() {
            if (this.params.page.page_number < this.params.page.max_pages) {
                this.params.page.page_number++;
                this.getProjects();
            }
        }
    },
    mounted() {
        this.getProjects();
    },
}
</script>

<template>
    <h3 class="pt-5 text-center">My projects</h3>
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
