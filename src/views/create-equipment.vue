// writen by xyh
<template>
  <div>
    <new-equipment-card></new-equipment-card>
  </div>
</template>

<script>
import newEquipmentCard from '../components/create-card/new-equipment-card'
export default {
  components: {
    'new-equipment-card': newEquipmentCard
  },
  created () {
    if (this.$store.getters.getUserKey === 'null') {
      this.$router.push('/login')
    }
  }
}
</script>
