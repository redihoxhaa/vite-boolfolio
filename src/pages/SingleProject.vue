<script>
// IMPORTS

import axios from 'axios';
import store from '../store';

// /IMPORTS

export default {
    props: [],
    components: {},
    data() {
        return {
            store,
            project: {},
            params: {
                slug: this.$route.params.slug
            }
        }
    },
    methods: {
        getProject() {
            axios.get(this.store.baseURL + this.store.URIs.projects + '/' + this.params.slug).then(response => {
                if (response.data.status) {
                    this.project = response.data.result;
                } else {
                    this.$router.push({ name: 'not-found' })
                }
            }).catch(
                error => {
                    console.log(error);
                }
            )
        },
    },
    created() {
        // Da aggiungere se vogliamo post linkati
        // this.$watch(
        //     () => this.$route.params,
        //     (toParams, previousParams) => {
        //         this.getProject();
        //     }),
        this.getProject();
    },
}
</script>

<template>
    <div class="card-custom mt-5" v-if="Object.keys(project).length">

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
