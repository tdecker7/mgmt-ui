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
                    <td v-if="editing === home.id">
                        <input type="text" v-model="home.name" />
                    </td>
                    <td v-else>{{ home.name }}</td>
                    <td v-if="editing === home.id">
                        <input type="text" v-model="home.address" />
                    </td>
                    <td v-else>{{ home.address }}</td>
                    <td v-if="editing === home.id">
                        <input type="text" v-model="home.type" />
                    </td>
                    <td v-else>{{ home.type }}</td>
                    <td v-if="editing === home.id">
                        <button @click="editHome(home)">Save</button>
                        <button class="muted-button" @click="cancelEdit(home)">Cancel</button>
                    </td>
                    <td v-else>
                        <button @click="editMode(home)">Edit</button>
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
            editMode(home) {
                this.cachedHome = Object.assign({}, home)
                this.editing = home.id;
            },
            editHome(home) {
                if (home.name === '' || home.address === '' || home.type === '') return
                this.$emit('edit:home', home.id, home)
                this.editing = null
            },
            cancelEdit(home) {
                Object.assign(home, this.cachedHome)
                this.editing = null
            }
        }
    }
</script>

<style scoped></style>