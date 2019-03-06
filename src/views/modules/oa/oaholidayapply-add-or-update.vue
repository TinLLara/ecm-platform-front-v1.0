<template>
  <el-dialog
    :title="!dataForm.id ? '新增' : '修改'"
    :close-on-click-modal="false"
    :visible.sync="visible">
    <el-form :model="dataForm" :rules="dataRule" ref="dataForm" @keyup.enter.native="dataFormSubmit()" label-width="80px">
    <el-form-item label="申请人" prop="applyperson">
      <el-input v-model="dataForm.applyperson" placeholder="申请人"></el-input>
    </el-form-item>
    <el-form-item label="申请时间" prop="applytime">
      <el-input v-model="dataForm.applytime" placeholder="申请时间"></el-input>
    </el-form-item>
    <el-form-item label="所属部门" prop="belongdept">
      <el-input v-model="dataForm.belongdept" placeholder="所属部门"></el-input>
    </el-form-item>
    <el-form-item label="员工编号" prop="staffnum">
      <el-input v-model="dataForm.staffnum" placeholder="员工编号"></el-input>
    </el-form-item>
    <el-form-item label="联系电话" prop="staffphone">
      <el-input v-model="dataForm.staffphone" placeholder="联系电话"></el-input>
    </el-form-item>
    <el-form-item label="邮箱地址" prop="stafftel">
      <el-input v-model="dataForm.stafftel" placeholder="邮箱地址"></el-input>
    </el-form-item>
    <el-form-item label="休假类型" prop="holidaytpye">
      <el-input v-model="dataForm.holidaytpye" placeholder="休假类型"></el-input>
    </el-form-item>
    <el-form-item label="起始时间" prop="starttime">
      <el-input v-model="dataForm.starttime" placeholder="起始时间"></el-input>
    </el-form-item>
    <el-form-item label="结束时间" prop="endtime">
      <el-input v-model="dataForm.endtime" placeholder="结束时间"></el-input>
    </el-form-item>
    <el-form-item label="" prop="starthour">
      <el-input v-model="dataForm.starthour" placeholder=""></el-input>
    </el-form-item>
    <el-form-item label="" prop="endhour">
      <el-input v-model="dataForm.endhour" placeholder=""></el-input>
    </el-form-item>
    <el-form-item label="天数" prop="days">
      <el-input v-model="dataForm.days" placeholder="天数"></el-input>
    </el-form-item>
    <el-form-item label="请休假原因" prop="reason">
      <el-input v-model="dataForm.reason" placeholder="请休假原因"></el-input>
    </el-form-item>
    <el-form-item label="附件" prop="holidayfile">
      <el-input v-model="dataForm.holidayfile" placeholder="附件"></el-input>
    </el-form-item>
    <el-form-item label="下一处理环节" prop="nextnode">
      <el-input v-model="dataForm.nextnode" placeholder="下一处理环节"></el-input>
    </el-form-item>
    <el-form-item label="下一处理人" prop="nextnoder">
      <el-input v-model="dataForm.nextnoder" placeholder="下一处理人"></el-input>
    </el-form-item>
    <el-form-item label="" prop="sendto">
      <el-input v-model="dataForm.sendto" placeholder=""></el-input>
    </el-form-item>
    <el-form-item label="年假总天数" prop="yholiday">
      <el-input v-model="dataForm.yholiday" placeholder="年假总天数"></el-input>
    </el-form-item>
    <el-form-item label="" prop="yused">
      <el-input v-model="dataForm.yused" placeholder=""></el-input>
    </el-form-item>
    <el-form-item label="" prop="iholiday">
      <el-input v-model="dataForm.iholiday" placeholder=""></el-input>
    </el-form-item>
    <el-form-item label="" prop="iused">
      <el-input v-model="dataForm.iused" placeholder=""></el-input>
    </el-form-item>
    <el-form-item label="已休其他假" prop="oused">
      <el-input v-model="dataForm.oused" placeholder="已休其他假"></el-input>
    </el-form-item>
    </el-form>
    <span slot="footer" class="dialog-footer">
      <el-button @click="visible = false">取消</el-button>
      <el-button type="primary" @click="dataFormSubmit()">确定</el-button>
    </span>
  </el-dialog>
</template>

<script>
  export default {
    data () {
      return {
        visible: false,
        dataForm: {
          happlyid: 0,
          applyperson: '',
          applytime: '',
          belongdept: '',
          staffnum: '',
          staffphone: '',
          stafftel: '',
          holidaytpye: '',
          starttime: '',
          endtime: '',
          starthour: '',
          endhour: '',
          days: '',
          reason: '',
          holidayfile: '',
          nextnode: '',
          nextnoder: '',
          sendto: '',
          yholiday: '',
          yused: '',
          iholiday: '',
          iused: '',
          oused: ''
        },
        dataRule: {
          applyperson: [
            { required: true, message: '申请人不能为空', trigger: 'blur' }
          ],
          applytime: [
            { required: true, message: '申请时间不能为空', trigger: 'blur' }
          ],
          belongdept: [
            { required: true, message: '所属部门不能为空', trigger: 'blur' }
          ],
          staffnum: [
            { required: true, message: '员工编号不能为空', trigger: 'blur' }
          ],
          staffphone: [
            { required: true, message: '联系电话不能为空', trigger: 'blur' }
          ],
          stafftel: [
            { required: true, message: '邮箱地址不能为空', trigger: 'blur' }
          ],
          holidaytpye: [
            { required: true, message: '休假类型不能为空', trigger: 'blur' }
          ],
          starttime: [
            { required: true, message: '起始时间不能为空', trigger: 'blur' }
          ],
          endtime: [
            { required: true, message: '结束时间不能为空', trigger: 'blur' }
          ],
          starthour: [
            { required: true, message: '不能为空', trigger: 'blur' }
          ],
          endhour: [
            { required: true, message: '不能为空', trigger: 'blur' }
          ],
          days: [
            { required: true, message: '天数不能为空', trigger: 'blur' }
          ],
          reason: [
            { required: true, message: '请休假原因不能为空', trigger: 'blur' }
          ],
          holidayfile: [
            { required: true, message: '附件不能为空', trigger: 'blur' }
          ],
          nextnode: [
            { required: true, message: '下一处理环节不能为空', trigger: 'blur' }
          ],
          nextnoder: [
            { required: true, message: '下一处理人不能为空', trigger: 'blur' }
          ],
          sendto: [
            { required: true, message: '不能为空', trigger: 'blur' }
          ],
          yholiday: [
            { required: true, message: '年假总天数不能为空', trigger: 'blur' }
          ],
          yused: [
            { required: true, message: '不能为空', trigger: 'blur' }
          ],
          iholiday: [
            { required: true, message: '不能为空', trigger: 'blur' }
          ],
          iused: [
            { required: true, message: '不能为空', trigger: 'blur' }
          ],
          oused: [
            { required: true, message: '已休其他假不能为空', trigger: 'blur' }
          ]
        }
      }
    },
    methods: {
      init (id) {
        this.dataForm.happlyid = id || 0
        this.visible = true
        this.$nextTick(() => {
          this.$refs['dataForm'].resetFields()
          if (this.dataForm.happlyid) {
            this.$http({
              url: this.$http.adornUrl(`/oa/oaholidayapply/info/${this.dataForm.happlyid}`),
              method: 'get',
              params: this.$http.adornParams()
            }).then(({data}) => {
              if (data && data.code === 0) {
                this.dataForm.applyperson = data.oaholidayapply.applyperson
                this.dataForm.applytime = data.oaholidayapply.applytime
                this.dataForm.belongdept = data.oaholidayapply.belongdept
                this.dataForm.staffnum = data.oaholidayapply.staffnum
                this.dataForm.staffphone = data.oaholidayapply.staffphone
                this.dataForm.stafftel = data.oaholidayapply.stafftel
                this.dataForm.holidaytpye = data.oaholidayapply.holidaytpye
                this.dataForm.starttime = data.oaholidayapply.starttime
                this.dataForm.endtime = data.oaholidayapply.endtime
                this.dataForm.starthour = data.oaholidayapply.starthour
                this.dataForm.endhour = data.oaholidayapply.endhour
                this.dataForm.days = data.oaholidayapply.days
                this.dataForm.reason = data.oaholidayapply.reason
                this.dataForm.holidayfile = data.oaholidayapply.holidayfile
                this.dataForm.nextnode = data.oaholidayapply.nextnode
                this.dataForm.nextnoder = data.oaholidayapply.nextnoder
                this.dataForm.sendto = data.oaholidayapply.sendto
                this.dataForm.yholiday = data.oaholidayapply.yholiday
                this.dataForm.yused = data.oaholidayapply.yused
                this.dataForm.iholiday = data.oaholidayapply.iholiday
                this.dataForm.iused = data.oaholidayapply.iused
                this.dataForm.oused = data.oaholidayapply.oused
              }
            })
          }
        })
      },
      // 表单提交
      dataFormSubmit () {
        this.$refs['dataForm'].validate((valid) => {
          if (valid) {
            this.$http({
              url: this.$http.adornUrl(`/oa/oaholidayapply/${!this.dataForm.happlyid ? 'save' : 'update'}`),
              method: 'post',
              data: this.$http.adornData({
                'happlyid': this.dataForm.happlyid || undefined,
                'applyperson': this.dataForm.applyperson,
                'applytime': this.dataForm.applytime,
                'belongdept': this.dataForm.belongdept,
                'staffnum': this.dataForm.staffnum,
                'staffphone': this.dataForm.staffphone,
                'stafftel': this.dataForm.stafftel,
                'holidaytpye': this.dataForm.holidaytpye,
                'starttime': this.dataForm.starttime,
                'endtime': this.dataForm.endtime,
                'starthour': this.dataForm.starthour,
                'endhour': this.dataForm.endhour,
                'days': this.dataForm.days,
                'reason': this.dataForm.reason,
                'holidayfile': this.dataForm.holidayfile,
                'nextnode': this.dataForm.nextnode,
                'nextnoder': this.dataForm.nextnoder,
                'sendto': this.dataForm.sendto,
                'yholiday': this.dataForm.yholiday,
                'yused': this.dataForm.yused,
                'iholiday': this.dataForm.iholiday,
                'iused': this.dataForm.iused,
                'oused': this.dataForm.oused
              })
            }).then(({data}) => {
              if (data && data.code === 0) {
                this.$message({
                  message: '操作成功',
                  type: 'success',
                  duration: 1500,
                  onClose: () => {
                    this.visible = false
                    this.$emit('refreshDataList')
                  }
                })
              } else {
                this.$message.error(data.msg)
              }
            })
          }
        })
      }
    }
  }
</script>
