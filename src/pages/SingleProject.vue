<script>
// IMPORTS

import axios from 'axios';

// /IMPORTS

export default {
    props: [],
    components: {},
    data() {
        return {
            project: [],
            baseURL: 'http://127.0.0.1:8000',
            URIs: {
                projects: '/api/projects'
            },
            params: {
                slug: this.$route.params.slug
            }
        }
    },
    methods: {
        getProject() {
            axios.get(this.baseURL + this.URIs.projects + '/' + this.params.slug).then(response => {
                if (Object.keys(response.data).length) {
                    this.project = response.data;
                } else {
                    // redirect alla pagina 404
                    this.$router.push({ name: 'not-found' })
                }
            })
        },
    },
    created() {
        this.getProject();
    },
}
</script>

<template>
    <div class="card-custom mt-5">

        <!-- Stauts progetto -->
        <p :class="[
            'header language fw-bold',
            {
                'text-success': project.status.title === 'Completed',
                'text-secondary': project.status.title === 'Ongoing',
                'text-danger': project.status.title === 'Aborted',
                'text-warning': project.status.title === 'Suspended'
            },
            'w-25',
            'text-lowercase'
        ]">
            {{ project.status.title }}
        </p>
        <div class="main-content">
            <!-- Titolo progetto -->
            <h3 class="title py-3">{{ project.title }}</h3>

            <!-- Data inizio progetto -->
            <p class="start-date pt-1">Project started on
                {{ project.start_date }}</p>

            <!-- Data fine progetto -->

            <p class="end-date" v-if="project.end_date">and ended on
                {{ project.end_date }}</p>


            <!-- Categoria progetto -->
            <p class="category text-uppercase badge bg-light text-black w-auto mx-auto my-3 p-2">
                {{ project.type.title }}
            </p>

            <!-- Linguaggi progetto -->


            <!-- Tecnologie progetto -->
            <div class="lang-container" v-if="project.technologies">

                <div class="skill-box" v-for="technology in project.technologies">
                    <span class="title">{{ technology.title }} </span>
                    <div class="skill-bar">
                        <span class="skill-per html">
                        </span>
                    </div>
                </div>

            </div>


        </div>


    </div>
</template>

<style lang="scss" scoped>
// USES

@use '../assets/scss/partials/components' as *;
@use '../assets/scss/partials/reset' as *;

// /USES
</style>
