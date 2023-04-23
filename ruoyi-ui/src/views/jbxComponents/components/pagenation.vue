<template>
  <div>
    <el-pagination
      @size-change="handleSizeChange"
      @current-change="handleCurrentChange"
      :current-page="currentPage"
      :page-sizes="[100, 200, 300, 400]"
      :page-size="100"
      layout="total, sizes, prev, pager, next, jumper"
      :total="400">
    </el-pagination>
  </div>
</template>
<script>
export default {
  name: 'radio',
  props: {
    currentPage: {
      type: Number,
      default: 4
    },
    pageSizes: {
      type: Number,
      default: 1
    },
    pageSize: {
      type: Number,
      default: 1
    },
    total: {
      type: Number,
      default: 99
    },
  },
  data () {
    return {
    }
  },
  methods: {
    handleSizeChange (val) {
      console.log(`每页 ${val} 条`)
    },
    handleCurrentChange (val) {
      console.log(`当前页: ${val}`)
    }
  }
}
</script>
<style lang="less" scoped>
</style>
