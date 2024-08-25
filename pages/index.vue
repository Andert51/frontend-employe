<template>
  <loginCard />
</template>

<script>
import loginCard from '~/components/employee/loginCard.vue'
export default {
  name: 'IndexPage',
  components: {
    loginCard
  },
  layout: 'login'
}
</script>
