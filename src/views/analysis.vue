<template>
  <div>
    <data-analysis></data-analysis>
  </div>
</template>

<script>
import dataAnalysis from '../components/data-analysis.vue'
export default {
  components: {
    'data-analysis': dataAnalysis
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
