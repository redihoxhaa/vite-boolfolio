<script>
import AppHeader from './components/AppHeader.vue'
import AppMain from './components/AppMain.vue'
import AppFooter from './components/AppFooter.vue'
import axios from 'axios'

export default {
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
  components: { AppHeader, AppMain, AppFooter },
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
  }
}
</script>

<template>
  <div class="container">
    <AppHeader />
    <AppMain :projects="projects" @prevPage="prevPage()" @nextPage="nextPage()" />
    <AppFooter />
  </div>
</template>

<style lang="scss" scoped></style>
