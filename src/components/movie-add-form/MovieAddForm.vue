<template >
    <Box>
        <h3>Yangi kino qo'shish</h3>
        <form class="add-form d-flex" @submit.prevent>
            <Input class="new-movie-label" placeholder="Qanday kino?" v-model="name" />
            <Input type="number" class="form-control new-movie-label" placeholder="Necha marotaba korilgan?" v-model="viewers" />
            <PrimaryButton type="submit" class="btn-outline-dark" @click="addMovie">Qo'shish</PrimaryButton>
        </form>
    </Box>
</template>
<script>
    export default {
        data() {
            return {
                name: '',
                viewers: ''
            }
        },
        methods: {
            addMovie() {
                if (!this.name || !this.viewers) return;
                const newMovie = {
                    id: Date.now(),
                    name: this.name,
                    viewers: this.viewers,
                    favourite: false,
                    like: false
                }
                this.$emit("createMovie", newMovie)
                this.name = ''
                this.viewers = ''
            },
        },
    }
</script>
<style>

</style>