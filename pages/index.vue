<template>
  <loginCard
    @show-alert="showAlert"
  />
</template>

<script>
import loginCard from '~/components/employee/loginCard.vue'
export default {
  name: 'IndexPage',
  components: {
    loginCard
  },
  layout: 'login',
  methods: {
    showAlert (data) {
      console.log('@Nint data => ', data)
      this.$nuxt.$emit('show-alert', data)
    }
  }
}
</script>
