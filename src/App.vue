<script>
import AppHeader from './components/AppHeader.vue'
import AppFooter from './components/AppFooter.vue'

export default {
  components: { AppHeader, AppFooter },
}
</script>

<template>
  <div class="container">
    <AppHeader />
    <router-view></router-view>
    <AppFooter />
  </div>
</template>

<style lang="scss" scoped></style>
