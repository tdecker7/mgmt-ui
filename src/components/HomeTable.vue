<template>
    <div id="home-table">
        <table>
            <thead>
                <tr>
                    <th>Home Name</th>
                    <th>Home Address</th>
                    <th>Home Type</th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="home in homes" :key="home.id">
                    <td>{{ home.name }}</td>
                    <td>{{ home.address }}</td>
                    <td>{{ home.type }}</td>
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
    }
</script>

<style scoped></style>