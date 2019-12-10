<template>
    <div id="home-table">
        <p v-if="homes.length < 1" class="empty-table">
            No homes
        </p>
        <table>
            <thead>
                <tr>
                    <th>Home Name</th>
                    <th>Home Address</th>
                    <th>Home Type</th>
                    <th>Actions</th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="home in homes" :key="home.id">
                    <td>{{ home.name }}</td>
                    <td>{{ home.address }}</td>
                    <td>{{ home.type }}</td>
                    <td>
                        <button @click="editMode(home.id)">Edit</button>
                        <button @click="$emit('delete:home', home.id)">Delete</button>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
</template>

<script>
    export default {
        name: 'home-table',
        props: {
            homes: Array,
        },
        data() {
            return {
                editing: null,
            }
        },
        methods: {
            editMode(id) {
                this.editing = id;
            },
            editHome(home) {
                if (home.name === '' || home.address === '' || home.type === '') return
                this.$emit('edit:home', home.id, home)
                this.editing = null
            }
        }
    }
</script>

<style scoped></style>