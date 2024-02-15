<script>
// IMPORTS

import ProjectCard from './ProjectCard.vue';

// /IMPORTS

export default {
  props: ['projects'],
  components: { ProjectCard },
  data() {
    return {

    }
  },
  methods: {},
  mounted() { },
}
</script>

<template>
  <h3 class="pt-5 text-center">My projects</h3>
  <ul class="row g-5">
    <li class="col-12 col-md-6 col-lg-4 d-flex" v-for="project in projects">
      <ProjectCard :project="project" />
    </li>
  </ul>
</template>

<style lang="scss" scoped>
// USES

@use '../assets/scss/partials/reset' as *;

// /USES
</style>
