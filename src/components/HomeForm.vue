<template>
    <div id="home-form">
        <form @submit.prevent="handleSubmit">
            <label>Home Name</label>
            <input v-model="home.name" type="text" />
            <label>Home Address</label>
            <input v-model="home.address" type="text" />
            <label>Home Type</label>
            <input v-model="home.type" type ="text" />
            <button>Add Home</button>
        </form>
    </div>
</template>

<script>
export default {
    name: 'home-form',
    data() {
        return {
            home: {
                name: '',
                address: '',
                type: '',
            },
        }
    },
    methods: {
        handleSubmit() {
            this.$emit('add:home', this.home)
        },
    },
}
</script>

<style scoped>
    form {
        margin-bottom: 2rem;
    }
</style>
