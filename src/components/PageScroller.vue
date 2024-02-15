<script>
// IMPORTS



// /IMPORTS

export default {
    props: [],
    components: {},
    emits: ['prevPage', 'nextPage'],
    data() {
        return {

        }
    },
    methods: {
    },
    mounted() { },
}
</script>

<template>
    <nav aria-label="Page navigation example" class="scroller my-5">
        <ul class="pagination d-flex justify-content-center">
            <li class="page-item" @click="$emit('prevPage')">

                <span aria-hidden="true" class="page-link">Previous</span>

            </li>
            <li class="page-item" @click="$emit('nextPage')">

                <span aria-hidden="true" class="page-link">Next</span>

            </li>
        </ul>
    </nav>
</template>

<style lang="scss" scoped>
// USES

// /USES

.page-link {
    color: white;
    background-color: #212121;
    cursor: pointer;
    user-select: none;
}
</style>
