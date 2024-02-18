<script>

// IMPORTS



// /IMPORTS

export default {
    props: [],
    components: {},
    data() {
        return {

        }
    },
    methods: {},
    mounted() { },
}
</script>

<template>
    <div class="d-flex justify-content-between align-items-center pt-5">
        <router-link :to="{ name: 'home' }" class="nav-link">
            <h1 class="text-uppercase text-center">Boolfolio</h1>
        </router-link>

        <div class="links d-flex gap-5">

            <router-link :to="{ name: 'projects' }" class="nav-link">
                <span>Projects</span>
            </router-link>

            <router-link :to="{ name: 'about' }" class="nav-link">
                <span>About</span>
            </router-link>
        </div>
    </div>
</template>

<style lang="scss" scoped>
// USES

@use '../assets/scss/partials/reset' as *;

// /USES
</style>
