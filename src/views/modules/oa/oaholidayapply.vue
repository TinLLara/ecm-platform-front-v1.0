<template>
  <div class="mod-config">
    <el-form :inline="true" :model="dataForm" @keyup.enter.native="getDataList()">
      <el-form-item>
        <el-input v-model="dataForm.key" placeholder="参数名" clearable></el-input>
      </el-form-item>
      <el-form-item>
        <el-button @click="getDataList()">查询</el-button>
        <el-button v-if="isAuth('oa:oaholidayapply:save')" type="primary" @click="addOrUpdateHandle()">新增</el-button>
        <el-button v-if="isAuth('oa:oaholidayapply:delete')" type="danger" @click="deleteHandle()" :disabled="dataListSelections.length <= 0">批量删除</el-button>
      </el-form-item>
    </el-form>
    <el-table
      :data="dataList"
      border
      v-loading="dataListLoading"
      @selection-change="selectionChangeHandle"
      style="width: 100%;">
      <el-table-column
        type="selection"
        header-align="center"
        align="center"
        width="50">
      </el-table-column>
      <!-- <el-table-column
        prop="happlyid"
        header-align="center"
        align="center"
        label="申请ID">
      </el-table-column> -->
      <el-table-column
        prop="applyperson"
        header-align="center"
        align="center"
        label="申请人">
      </el-table-column>
      <el-table-column
        prop="applytime"
        header-align="center"
        align="center"
        label="申请时间">
      </el-table-column>
      <el-table-column
        prop="belongdept"
        header-align="center"
        align="center"
        label="所属部门">
      </el-table-column>
      <el-table-column
        prop="staffnum"
        header-align="center"
        align="center"
        label="员工编号">
      </el-table-column>
      <el-table-column
        prop="staffphone"
        header-align="center"
        align="center"
        label="联系电话">
      </el-table-column>
      <el-table-column
        prop="stafftel"
        header-align="center"
        align="center"
        label="邮箱地址">
      </el-table-column>
      <el-table-column
        prop="holidaytpye"
        header-align="center"
        align="center"
        label="休假类型">
      </el-table-column>
      <el-table-column
        prop="starttime"
        header-align="center"
        align="center"
        label="起始时间"
        >
      </el-table-column>
      <el-table-column
        prop="endtime"
        header-align="center"
        align="center"
        label="结束时间">
      </el-table-column>
      <!-- <el-table-column
        prop="starthour"
        header-align="center"
        align="center"
        label="">
      </el-table-column>
      <el-table-column
        prop="endhour"
        header-align="center"
        align="center"
        label="">
      </el-table-column> -->
      <el-table-column
        prop="days"
        header-align="center"
        align="center"
        label="天数">
      </el-table-column>
      <!-- <el-table-column
        prop="reason"
        header-align="center"
        align="center"
        label="请休假原因">
      </el-table-column>
      <el-table-column
        prop="holidayfile"
        header-align="center"
        align="center"
        label="附件">
      </el-table-column>
      <el-table-column
        prop="nextnode"
        header-align="center"
        align="center"
        label="下一处理环节">
      </el-table-column>
      <el-table-column
        prop="nextnoder"
        header-align="center"
        align="center"
        label="下一处理人">
      </el-table-column>
      <el-table-column
        prop="sendto"
        header-align="center"
        align="center"
        label="">
      </el-table-column>
      <el-table-column
        prop="yholiday"
        header-align="center"
        align="center"
        label="年假总天数">
      </el-table-column>
      <el-table-column
        prop="yused"
        header-align="center"
        align="center"
        label="">
      </el-table-column>
      <el-table-column
        prop="iholiday"
        header-align="center"
        align="center"
        label="">
      </el-table-column>
      <el-table-column
        prop="iused"
        header-align="center"
        align="center"
        label="">
      </el-table-column>
      <el-table-column
        prop="oused"
        header-align="center"
        align="center"
        label="已休其他假">
      </el-table-column> -->
      <el-table-column
        fixed="right"
        header-align="center"
        align="center"
        width="150"
        label="操作">
        <template slot-scope="scope">
          <el-button type="text" size="small" @click="addOrUpdateHandle(scope.row.happlyid)">修改</el-button>
          <el-button type="text" size="small" @click="deleteHandle(scope.row.happlyid)">删除</el-button>
        </template>
      </el-table-column>
    </el-table>
    <el-pagination
      @size-change="sizeChangeHandle"
      @current-change="currentChangeHandle"
      :current-page="pageIndex"
      :page-sizes="[10, 20, 50, 100]"
      :page-size="pageSize"
      :total="totalPage"
      layout="total, sizes, prev, pager, next, jumper">
    </el-pagination>
    <!-- 弹窗, 新增 / 修改 -->
    <add-or-update v-if="addOrUpdateVisible" ref="addOrUpdate" @refreshDataList="getDataList"></add-or-update>
  </div>
</template>

<script>
  import AddOrUpdate from './oaholidayapply-add-or-update'
  export default {
    data () {
      return {
        dataForm: {
          key: ''
        },
        dataList: [],
        pageIndex: 1,
        pageSize: 10,
        totalPage: 0,
        dataListLoading: false,
        dataListSelections: [],
        addOrUpdateVisible: false
      }
    },
    components: {
      AddOrUpdate
    },
    activated () {
      this.getDataList()
    },
    methods: {
      // 获取数据列表
      getDataList () {
        this.dataListLoading = true
        this.$http({
          url: this.$http.adornUrl('/oa/oaholidayapply/list'),
          method: 'get',
          params: this.$http.adornParams({
            'page': this.pageIndex,
            'limit': this.pageSize,
            'key': this.dataForm.key
          })
        }).then(({data}) => {
          if (data && data.code === 0) {
            this.dataList = data.page.list
            this.totalPage = data.page.totalCount
          } else {
            this.dataList = []
            this.totalPage = 0
          }
          this.dataListLoading = false
        })
      },
      // 每页数
      sizeChangeHandle (val) {
        this.pageSize = val
        this.pageIndex = 1
        this.getDataList()
      },
      // 当前页
      currentChangeHandle (val) {
        this.pageIndex = val
        this.getDataList()
      },
      // 多选
      selectionChangeHandle (val) {
        this.dataListSelections = val
      },
      // 新增 / 修改
      addOrUpdateHandle (id) {
        this.addOrUpdateVisible = true
        this.$nextTick(() => {
          this.$refs.addOrUpdate.init(id)
        })
      },
      // 删除
      deleteHandle (id) {
        var ids = id ? [id] : this.dataListSelections.map(item => {
          return item.happlyid
        })
        this.$confirm(`确定对[id=${ids.join(',')}]进行[${id ? '删除' : '批量删除'}]操作?`, '提示', {
          confirmButtonText: '确定',
          cancelButtonText: '取消',
          type: 'warning'
        }).then(() => {
          this.$http({
            url: this.$http.adornUrl('/oa/oaholidayapply/delete'),
            method: 'post',
            data: this.$http.adornData(ids, false)
          }).then(({data}) => {
            if (data && data.code === 0) {
              this.$message({
                message: '操作成功',
                type: 'success',
                duration: 1500,
                onClose: () => {
                  this.getDataList()
                }
              })
            } else {
              this.$message.error(data.msg)
            }
          })
        })
      }
    }
  }
</script>
