<template>
  <v-dialog
    v-model="showDialog"
    width="300"
    color="gray"
    persistent
  >
    <v-card>
      <v-card-title>
        Delete Employee
      </v-card-title>
      <v-card-text>
        Are you Sure?
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
          <v-btn color="red" @click="deleteEmployee">
            Delete
          </v-btn>
        </v-row>
      </v-card-actions>
    </v-card>
  </v-dialog>
</template>

<script>
export default {
  props: {
    idEmployee: { type: String, default: null }
  },
  data () {
    return {
      showDialog: true
    }
  },
  mounted () {
    console.log('@Nint id => ', this.idEmployee)
  },
  methods: {
    closeDialog () {
      this.showDialog = false
      this.$emit('close')
    },
    async deleteEmployee () {
      console.log('@Nint id-delete => ', this.idEmployee)
      const res = await this.$axios.delete(`/delete/${this.idEmployee}`)
      if (res.data.succes) {
        this.$emit('update')
      }
      console.log('@Nint response => ', res)
    }
  }
}
</script>

<style scoped>

</style>
