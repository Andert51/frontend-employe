<template>
  <v-dialog
    v-model="showDialog"
    width="800"
  >
    <v-card style="color: gray;">
      <v-card-title>
        Add a new Employee
      </v-card-title>
      <v-card-text>
        <v-form ref="formCreated">
          <v-row>
            <v-col cols="12" md="6">
              <v-text-field
                v-model="employee.nombre"
                placeholder="Write your name"
                label="Name"
                filled
                dense
                color="accent"
                outlined
                :rules="[rule.required]"
                class="animate__animated animate__fadeInLeft"
              />
            </v-col>
            <v-col cols="12" md="6">
              <v-text-field
                v-model="employee.apaterno"
                placeholder="Write your Paternal surname"
                label="Paternal Surname"
                filled
                dense
                color="accent"
                outlined
                :rules="[rule.required]"
                class="animate__animated animate__fadeInRight"
              />
            </v-col>
          </v-row>
          <v-row>
            <v-col cols="12" md="6">
              <v-text-field
                v-model="employee.amaterno"
                placeholder="Write your Maternal surname"
                label="Maternal Surname"
                filled
                dense
                color="accent"
                outlined
                :rules="[rule.required]"
                class="animate__animated animate__fadeInLeft"
              />
            </v-col>
            <v-col cols="12" md="6">
              <v-text-field
                v-model="employee.direccion"
                placeholder="Write your Direction"
                label="Direction"
                filled
                dense
                color="accent"
                outlined
                :rules="[rule.required]"
                class="animate__animated animate__fadeInRight"
              />
            </v-col>
          </v-row>
          <v-row>
            <v-col cols="12" md="6">
              <v-text-field
                v-model="employee.telefono"
                placeholder="Write your Phone number"
                label="Phone"
                filled
                dense
                color="accent"
                outlined
                :rules="[rule.required]"
                class="animate__animated animate__fadeInLeft"
              />
            </v-col>
            <v-col cols="12" md="6">
              <v-text-field
                v-model="employee.ciudad"
                placeholder="Write your City"
                label="City"
                filled
                dense
                color="accent"
                outlined
                :rules="[rule.required]"
                class="animate__animated animate__fadeInRight"
              />
            </v-col>
          </v-row>
          <v-row>
            <v-col cols="12" md="6">
              <v-text-field
                v-model="employee.estado"
                placeholder="Write your State"
                label="State"
                filled
                dense
                color="accent"
                outlined
                :rules="[rule.required]"
                class="animate__animated animate__fadeInLeft"
              />
            </v-col>
            <v-col cols="12" md="6">
              <v-text-field
                v-model="employee.correo"
                placeholder="Write your Mail"
                label="Mail"
                filled
                dense
                color="accent"
                outlined
                :rules="[rule.required, rule.mail]"
                class="animate__animated animate__fadeInRight"
              />
            </v-col>
          </v-row>
          <v-row>
            <v-col cols="12" md="6">
              <v-text-field
                v-model="employee.contrasena"
                placeholder="Write your Password (Password must be at least 6 characters)"
                label="Password"
                filled
                dense
                color="accent"
                outlined
                :rules="[rule.required, rule.size]"
                type="password"
                class="animate__animated animate__fadeInRight"
              />
            </v-col>
            <v-col cols="4">
              <v-combobox
                v-model="employee.perfil"
                :items="rols"
                dense
                outlined
                filled
              />
            </v-col>
          </v-row>
        </v-form>
      </v-card-text>
      <v-card-actions>
        <v-row
          align="center"
          justify="center"
          class="pa-2 ma-2"
        >
          <v-btn color="green" @click="closeDialog">
            Cancel
          </v-btn>
          |
          <v-btn color="red" @click="createEmployee">
            Add
          </v-btn>
        </v-row>
      </v-card-actions>
    </v-card>
  </v-dialog>
</template>

<script>
export default {
  data () {
    return {
      showDialog: true,
      employee: {},
      rols: ['admin', 'rh', 'conta', 'systems'],
      rule: {
        required: val => (val || '').length > 0 || 'This field is required',
        size: val => (val || '').length > 6 || 'At least 6 chars password',
        mail: val => /^\w+([.-]?\w+)*@\w+([.-]?\w+)*(\.\w{2,3})+$/.test(val) || 'Mail must be valid'
      }

    }
  },
  mounted () {
    this.employee.perfil = 'admin'
  },
  methods: {
    closeDialog () {
      this.showDialog = false
      this.$emit('close')
    },
    async createEmployee () {
      const isValid = this.$refs.formCreated.validate()
      if (isValid) {
        this.employee.noempleado = new Date()
        const res = await this.$axios.post('/create', this.employee)
        console.log('@Nint res => ', res)
        if (res.data.succes) {
          this.$emit('update')
        }
      }
    }
  }
}

</script>

<style scoped>

</style>
