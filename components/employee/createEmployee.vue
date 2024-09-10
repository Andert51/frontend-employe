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
        Pending
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
      showDialog: true
    }
  },
  methods: {
    closeDialog () {
      this.showDialog = false
      this.$emit('close')
    },
    createEmployee () {
      // pending
    }
  }
}

</script>

<style scoped>

</style>
