<template>
  <div>
    <v-row align="center" justify="center">
      <h1>CRUD Employee</h1>
    </v-row>
    <v-row align="center" justify="center">
      <v-data-table
        style="width: 100%;"
        :headers="headers"
        :items="employee"
      />
    </v-row>
  </div>
</template>

<script>
export default {
  data () { // Crear, momtar, similar a DOM content loaded
    return {
      employee: [],
      headers: [
        {
          text: 'Name',
          align: 'center',
          sortable: true,
          value: 'nombre'
        },
        {
          text: 'Pat. Surname',
          align: 'center',
          sortable: true,
          value: 'apaterno'
        },
        {
          text: 'Mat. Surname',
          align: 'center',
          sortable: true,
          value: 'apaterno'
        },
        {
          text: 'Adress',
          align: 'center',
          sortable: true,
          value: 'direccion'
        },
        {
          text: 'Phone',
          align: 'center',
          sortable: true,
          value: 'telefono'
        },
        {
          text: 'City',
          align: 'center',
          sortable: true,
          value: 'ciudad'
        },
        {
          text: 'State',
          align: 'center',
          sortable: true,
          value: 'estado'
        },
        {
          text: 'Mail',
          align: 'center',
          sortable: true,
          value: 'correo'
        },
        {
          text: 'Employee No.',
          align: 'center',
          sortable: true,
          value: 'noempleado'
        },
        {
          text: 'User',
          align: 'center',
          sortable: true,
          value: 'perfil'
        }
      ]
    }
  },

  mounted () {
    this.loadEmployee()
  },
  methods: {
    async loadEmployee () {
      const response = await this.$axios.get('/get-all')
      if (response.data.succes === true) {
        // this.employee = response.data.message
        response.data.message.forEach((item) => {
          this.employee.push(item)
        })
      }
      console.log('@Nint response => ', response)
    }
  }

}

</script>

<style scoped>

</style>
