// writen by xyh
<template>
  <div>
    <el-card class='title-card'>所有设备</el-card>
    <!-- <search-filter :options="options"
                   @search="searchAndFilter"></search-filter> -->
    <el-card class="table-card">
      <el-table :data="equipmentList"
                stripe
                @row-click="enterEquipment"
                id="equipment-table"
                class="table"
                :height="height">
        <el-table-column prop="id"
                         label="ID"
                         width="40">
        </el-table-column>
        <el-table-column prop="name"
                         label="设备名"
                         width="180">
        </el-table-column>
        <el-table-column prop="created_at"
                         label="上架时间"
                         width="180">
        </el-table-column>
        <el-table-column prop="address"
                         label="地址"
                         width="180">
        </el-table-column>
        <el-table-column prop="email"
                         label="Email"
                         width="180">
        </el-table-column>
        <el-table-column prop="phone"
                         label="电话号码"
                         width="180">
        </el-table-column>
        <el-table-column prop="status"
                         label="状态"
                         width="180">
        </el-table-column>
      </el-table>
    </el-card>
  </div>
</template>

<style scoped>
.title-card {
  margin: auto;
  margin-top: 20px;
  position: relative;
}
.table {
  position: relative;
  margin: 0 auto;
}
.page-chooser {
  position: relative;
  margin: 10px auto;
  left: 40%;
}
</style>

<script>
import Axios from 'axios'
// import searchAndFilter from '../search&filter'
export default {
  components: {
    // 'search-filter': searchAndFilter
  },
  props: {
    userId: Number,
    pageSize: Number,
    height: Number
  },
  data: function () {
    return {
      equipmentList: [],
      options: [
        { value: 'search', label: '全部搜索' },
        { value: 'equipment', label: '筛选：设备名' },
        { value: 'address', label: '筛选：地址' },
        { value: 'email', label: '筛选：邮箱' },
        { value: 'phone', label: '筛选：电话' }
      ],
      select: 'search',
      input: '',
      data: { count: 0 }
    }
  },
  created: function () {
    this.changePage()
  },
  methods: {

    enterEquipment: function (row) {
      this.$router.push({ name: 'equipment', params: { equipmentId: row.id } })
    },
    searchAndFilter: function (select, input) {
      this.input = input
      this.select = select
      this.changePage()
    },
    changePage: function () {
      if (this.$store.getters.getUserKey === 'null') {
        return
      }

      Axios.get('/api/v1/user/' + this.userId + '/', {
        headers: {
          Authorization: 'Token ' + this.$store.getters.getUserKey
        }
      })
        .then((response) => {
          this.equipmentList = response.data.rented_equipments
          this.data = response.data
        }).catch((error) => {
          // alert('error:' + error)
          console.log(error)
          this.$alert(error.response.data)
        })
    }
  }
}
</script>
