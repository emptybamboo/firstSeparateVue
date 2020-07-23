<template>
  <div>
    <div>
      <el-table
        :data="tableData"
        border
        style="width: 80%;margin-left: 100px;margin-top: 30px;">
        <el-table-column
          fixed
          prop="id"
          label="编号"
          width="100">
        </el-table-column>
        <el-table-column
          prop="name"
          label="图书"
          width="150">
        </el-table-column>
        <el-table-column
          prop="author"
          label="作者"
          width="150">
        </el-table-column>
        <el-table-column
          prop="publish"
          label="出版社"
          width="180">
        </el-table-column>
        <el-table-column
          prop="pages"
          label="总页数"
          width="100">
        </el-table-column>
        <el-table-column
          prop="price"
          label="价格"
          width="100">
        </el-table-column>
        <el-table-column
          prop="bookCase.name"
          label="分类"
          width="120">
        </el-table-column>
        <el-table-column
          fixed="right"
          label="操作"
          width="100">
          <template slot-scope="scope">
            <el-button type="text" size="small">修改</el-button>
            <el-button type="text" size="small">删除</el-button>
          </template>
        </el-table-column>

      </el-table>
      <el-pagination
        background
        layout="prev, pager, next"
        :total="total"
        :page-size="pageSize"
        @current-change="change"
      >
      </el-pagination>
    </div>
  </div>
</template>

<script>
export default {
  methods: {
    change (currentPage) {
      this.currentPage = currentPage
      const _this = this
      // eslint-disable-next-line no-undef
      this.$ajax.get('http://localhost:8181/book/findByPage/' + currentPage).then(function (resp) {
        _this.tableData = resp.data.data
      })
    }
  },

  data () {
    return {
      total: 0,
      pageSize: 5,
      tableData: [],
      currentPage: 0
    }
  },

  created () {
    const _this = this
    // eslint-disable-next-line no-undef
    this.$ajax.get('http://localhost:8181/book/findByPage/1').then(function (resp) {
      console.log(resp.data)
      _this.pageSize = resp.data.pageSize
      _this.total = resp.data.total
      _this.tableData = resp.data.data
    })
  }
}
</script>

<style scoped>

</style>
