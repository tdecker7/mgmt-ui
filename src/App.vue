<template>
  <div id="app" class="small-container">
    <h1>Homes</h1>
    <home-table :homes="homes" @delete:home="deleteHome"/>
    <home-form @add:home="addHome" />
  </div>
</template>

<script>
import HomeTable from '@/components/HomeTable.vue'
import HomeForm from '@/components/HomeForm.vue'

export default {
  name: 'app',
  components: {
    HomeTable,
    HomeForm
  },
  data() {
    return {
      homes: [
        {
          id: 1,
          name: 'Lehigh House',
          address: '1111 Lehigh',
          type: 'Main Residence',
        },
        {
          id: 2,
          name: 'Nort Woods Cabin',
          address: '1111 Woodsy Lane',
          type: 'Vacation Home',
        },
        {
          id: 3,
          name: 'Bachelor Pad',
          address: '1111 Marmaduke Ave',
          type: 'Rental Property',
        },
      ],
    }
  },
  methods: {
    addHome(home) {
      this.homes = [...this.homes, home]
    },
    deleteHome(id) {
      this.homes = this.homes.filter(
        home => home.id !== id
      )
    }
  }
}
</script>

<style>
/* #app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
} */
  button {
    background: #009435;
    border: 1px solid #009435;
  }

  .small-container {
    max-width: 680px;
  }
</style>
