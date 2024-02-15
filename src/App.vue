<script>
import AppHeader from './components/AppHeader.vue'
import AppMain from './components/AppMain.vue'
import AppFooter from './components/AppFooter.vue'
import axios from 'axios'

export default {
  data() {
    return {
      baseURL: 'http://127.0.0.1:8000',
      URIs: {
        projects: '/api/projects'
      }
    }
  },
  components: { AppHeader, AppMain, AppFooter },
  methods: {
    getProjects() {
      axios.get(this.baseURL + this.URIs.projects).then(response => {
        console.log(response);
      })
    }
  },
  mounted() {
    this.getProjects();
  }
}
</script>

<template>
  <AppHeader />
  <AppMain />
  <AppFooter />
</template>

<style lang="scss" scoped></style>
