<script>
// IMPORTS
import store from '../store';


// /IMPORTS

export default {
    props: [],
    components: {},
    data() {
        return {
            store
        }
    },
    emits: ['searchProject'],
    methods: {
        search() {
            this.$emit('searchProject');
            this.$router.push({ name: 'projects', query: { page: 1, key: this.store.searchKey } });
        }
    },
    mounted() { },
}
</script>

<template>
    <div class="form-floating my-3">
        <input type="text" class="form-control" id="searchInput" placeholder="Search" v-model="store.searchKey">
        <label for="searchInput">Search</label>
    </div>
    <button class="custom-btn orange p-2" @click="search()">Search</button>
</template>

<style lang="scss" scoped>
// USES
@use '../assets/scss/partials/components' as *;
@use '../assets/scss/partials/reset' as *;


// /USES
</style>
