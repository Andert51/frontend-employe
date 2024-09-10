<template>
  <div style="width: 100%; padding:0; margin:0;">
    <v-row align="center" justify="center">
      <h1>CRUD Employee</h1>
    </v-row>
    <v-row
      align="center"
      justify="end"
      style="margin-top:10px; margin-bottom: 10px;"
    >
      <v-btn
        color="primary"
        @click="createEmployee"
      >
        <v-icon>mdi-account</v-icon>
        <span style="text-transform: none;">
          Create Employee
        </span>
      </v-btn>
    </v-row>
    <v-row align="center" justify="center">
      <v-data-table
        style="width: 100%;"
        :headers="headers"
        :items="employee"
      >
        <template #[`item.actions`]="{ item }">
          <v-tooltip bottom color="orange">
            <template #activator="{on, attrs }">
              <v-btn
                icon
                color="warning"
                v-bind="attrs"
                :disabled="item.perfil === 'admin'"
                @click="updateEmployee(item)"
                v-on="on"
              >
                <v-icon>
                  mdi-update
                </v-icon>
              </v-btn>
            </template>
            <span>
              Update Employee: {{ item.nombre }}
            </span>
          </v-tooltip>
          |
          <v-tooltip bottom color="red">
            <template #activator="{on, attrs }">
              <v-btn
                icon
                color="red"
                v-bind="attrs"
                :disabled="item.perfil === 'admin'"
                @click="deleteEmployee(item.id)"
                v-on="on"
              >
                <v-icon>
                  mdi-delete
                </v-icon>
              </v-btn>
            </template>
            <span>
              Delete Employee: {{ item.nombre }}
            </span>
          </v-tooltip>
        </template>
      </v-data-table>
    </v-row>
    <delete-employee
      v-if="showDelete"
      :id-employee="idEmployee"
      @close="destroyComponet"
      @update="updateTable"
    />
    <create-employee
      v-if="showCreate"
      @close="destroyCreate"
    />
  </div>
</template>

<script>
import deleteEmployee from '~/components/employee/deleteEmployee.vue'
import createEmployee from '~/components/employee/createEmployee.vue'
export default {
  components: {
    deleteEmployee,
    createEmployee
  },
  data () { // Crear, momtar, similar a DOM content loaded
    return {
      employee: [],
      headers: [
        {
          text: 'Employee No.',
          align: 'center',
          sortable: true,
          value: 'noempleado'
        },
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
          text: 'Rol',
          align: 'center',
          sortable: true,
          value: 'perfil'
        },
        {
          text: 'Actions',
          align: 'center',
          sortable: false,
          value: 'actions'
        }
      ],
      showDelete: false,
      idEmployee: null,
      showCreate: false
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
        this.employee = []
        response.data.message.forEach((item) => {
          this.employee.push(item)
        })
      }
      console.log('@Nint response => ', response)
    },
    deleteEmployee (id) {
      this.idEmployee = id
      this.showDelete = true
    },
    destroyComponet () {
      this.showDelete = false
      this.idEmployee = null
    },
    updateTable () {
      this.showDelete = false
      this.idEmployee = null
      this.loadEmployee()
    },
    destroyCreate () {
      this.showCreate = false
    },
    createEmployee () {
      this.showCreate = true
    }
  }

}

</script>

<style scoped>

</style>
