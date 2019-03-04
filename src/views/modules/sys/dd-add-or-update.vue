<template>
  <el-dialog
    :title="!dataForm.id ? '新增' : '修改'"
    :close-on-click-modal="false"
    :visible.sync="visible">
    <el-form :model="dataForm" :rules="dataRule" ref="dataForm" @keyup.enter.native="dataFormSubmit()" label-width="80px">
    <el-form-item label="字典编码" prop="ddKey">
      <el-input v-model="dataForm.ddKey" placeholder="字典编码"></el-input>
    </el-form-item>
    <el-form-item label="字典名称" prop="ddLabel">
      <el-input v-model="dataForm.ddLabel" placeholder="字典名称"></el-input>
    </el-form-item>
    <el-form-item label="字典取值" prop="ddValue">
      <el-input v-model="dataForm.ddValue" placeholder="字典取值"></el-input>
    </el-form-item>
    <el-form-item label="顺序号" prop="seqNo">
      <el-input v-model="dataForm.seqNo" placeholder="顺序号"></el-input>
    </el-form-item>
    <!-- <el-form-item label="创建时间" prop="createTime">
      <el-input v-model="dataForm.createTime" placeholder="创建时间"></el-input>
    </el-form-item>
    <el-form-item label="修改时间" prop="updateTime">
      <el-input v-model="dataForm.updateTime" placeholder="修改时间"></el-input>
    </el-form-item> -->
    <el-form-item label="是否可用" prop="isEnable">
      <el-input v-model="dataForm.isEnable" placeholder="是否可用"></el-input>
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
          id: 0,
          ddKey: '',
          ddLabel: '',
          ddValue: '',
          seqNo: '',
          // createTime: '',
          // updateTime: '',
          isEnable: ''
        },
        dataRule: {
          ddKey: [
            { required: true, message: '字典编码不能为空', trigger: 'blur' }
          ],
          ddLabel: [
            { required: true, message: '字典名称不能为空', trigger: 'blur' }
          ],
          ddValue: [
            { required: true, message: '字典取值不能为空', trigger: 'blur' }
          ],
          seqNo: [
            { required: true, message: '顺序号不能为空', trigger: 'blur' }
          ],
          // createTime: [
          //   { required: true, message: '创建时间不能为空', trigger: 'blur' }
          // ],
          // updateTime: [
          //   { required: true, message: '修改时间不能为空', trigger: 'blur' }
          // ],
          isEnable: [
            { required: true, message: '是否可用不能为空', trigger: 'blur' }
          ]
        }
      }
    },
    methods: {
      init (id) {
        this.dataForm.id = id || 0
        this.visible = true
        this.$nextTick(() => {
          this.$refs['dataForm'].resetFields()
          if (this.dataForm.id) {
            this.$http({
              url: this.$http.adornUrl(`/generator/sysddvalue/info/${this.dataForm.id}`),
              method: 'get',
              params: this.$http.adornParams()
            }).then(({data}) => {
              if (data && data.code === 0) {
                this.dataForm.ddKey = data.sysddvalue.ddKey
                this.dataForm.ddLabel = data.sysddvalue.ddLabel
                this.dataForm.ddValue = data.sysddvalue.ddValue
                this.dataForm.seqNo = data.sysddvalue.seqNo
                // this.dataForm.createTime = data.sysddvalue.createTime
                // this.dataForm.updateTime = data.sysddvalue.updateTime
                this.dataForm.isEnable = data.sysddvalue.isEnable
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
              url: this.$http.adornUrl(`/generator/sysddvalue/${!this.dataForm.id ? 'save' : 'update'}`),
              method: 'post',
              data: this.$http.adornData({
                'id': this.dataForm.id || undefined,
                'ddKey': this.dataForm.ddKey,
                'ddLabel': this.dataForm.ddLabel,
                'ddValue': this.dataForm.ddValue,
                'seqNo': this.dataForm.seqNo,
                // 'createTime': this.dataForm.createTime,
                // 'updateTime': this.dataForm.updateTime,
                'isEnable': this.dataForm.isEnable
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
