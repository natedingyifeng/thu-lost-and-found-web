<template>
  <div>
    <account-create></account-create>
  </div>
</template>

<script>
import accountCreation from '../components/account_creation.vue'
export default {
  components: {
    'account-create': accountCreation
  },
  data: function () {
    return {

    }
  },
  created () {
    if(this.$store.getters.getUserLoginStatus != "true")
    {
      this.$router.push('/login')
    }
  }
}
</script>
