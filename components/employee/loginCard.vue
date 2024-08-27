<template>
  <v-card
    elevation="0"
    color="teal lighten-3 "
    width="400"
    height="300"
    rounded
  >
    <v-card-title>
      <v-row align="center" justify="center">
        <span style="color:white;">
          <h3>LogIn</h3>
        </span>
      </v-row>
    </v-card-title>
    <v-card-text class="mt-4 mb-4 pt-4 pb-4">
      <v-form ref="form">
        <div class="textFields">
          <v-row style="width: 100%;">
            <v-text-field
              v-model="usuario"
              placeholder="User"
              :rules="size"
              solo
            />
          </v-row>
          <v-row style="width: 100%;">
            <v-text-field
              v-model="password"
              placeholder="Password"
              :rules="size"
              type="password"
              solo
            />
          </v-row>
        </div>
      </v-form>
    </v-card-text>
    <v-card-actions>
      <v-row align="center" justify="center">
        <v-btn
          color="cyan lighten-4"
          @click="loginBackend"
        >
          <span style="text-transform: none; color:black;">
            Login
          </span>
          <v-icon style="color: black;">
            mdi-login-variant
          </v-icon>
        </v-btn>
      </v-row>
    </v-card-actions>
  </v-card>
</template>

<script>
export default {
  data () {
    return {
      usuario: '',
      password: '',
      size: [
        v => v.trim().length !== 0 || 'No puede estar vacio' // Mensaje para recuadro
      ]
    }
  },
  methods: {
    loginBackend () {
      console.log('@Nint variables', this.usuario, this.password)
      const isValid = this.$refs.form.validate()
      if (isValid) {
        const body = {
          correo: this.usuario,
          contrasena: this.password
        }
        this.$axios.post('/login', body)
          .then((res) => {
            console.log('@Nint res => ', res)
          })
          .catch((error) => {
            console.error('@Nint error =>', error)
          })
      } else {
        this.$emit('show-alert', {
          showAlert: true,
          color: 'red',
          type: 'error',
          message: 'Invalid Credentials',
          icon: 'mdi-error',
          border: 'white'
        })
      }
    }
  }
}
</script>

<style scoped>
.textFields {
    width: 100%;
    margin: 10px;
}
</style>
