<template>
    <nav aria-label="pagination">
        <ul class="pagination pagination-sm">
            <li v-for="pageNuber in totalPages" :key="pageNuber" :class="{'active': pageNuber == page}" @click="changePageHandler(pageNuber)">
                <span class="page-link fs-5">{{ pageNuber }}</span>
            </li>
        </ul>
    </nav>
</template>
<script>
    export default {
        props: {
            totalPages: {
                type: Number,
                required: true
            },
            currentPage: {
                type: Number,
                required: true,
            },
            changePageHandler: {
                type: Function,
                required: true
            },
            page: {
                type: Number,
                required: true
            }
        }
    }
</script>
<style>

</style>