// writen by xyh
<template>
  <div>
    <renter-application-card :id="id"></renter-application-card>
  </div>
</template>

<script>
import renterApplicationCard from '../components/card/renter-application-card'
export default {
  components: {
    'renter-application-card': renterApplicationCard
  },
  data: function () {
    return {
      id: parseInt(this.$route.params.renterApplicationId)
    }
  },
  created () {
    if (this.$store.getters.getUserKey === 'null') {
      this.$router.push('/login')
    }
  }
}
</script>
