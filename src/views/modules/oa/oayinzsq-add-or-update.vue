<template>
  <el-dialog
    :title="!dataForm.id ? '新增' : '修改'"
    :close-on-click-modal="false"
    :visible.sync="visible">
    <el-form :inline="true" :model="dataForm" :rules="dataRule" ref="dataForm" @keyup.enter.native="dataFormSubmit()" label-width="80px">
    <el-form-item label="起草人" prop="appname">
      <el-input v-model="dataForm.appname" placeholder="起草人"></el-input>
    </el-form-item>
    <el-form-item label="起草时间" prop="appdate">
      <el-input v-model="dataForm.appdate" placeholder="起草时间"></el-input>
    </el-form-item>
    <el-form-item label="所在部门">
      <!-- <el-input v-model="dataForm.depart" placeholder="所在部门"></el-input> -->
      <el-select v-model="dataForm.depart" placeholder="所在部门">
        <el-option label="管理委员会" value="1"></el-option>
        <el-option label="前台部门" value="2"></el-option>
        <el-option label="中台部门" value="3"></el-option>
        <el-option label="后台部门" value="4"></el-option>
      </el-select>
    </el-form-item>
    <el-form-item label="用印份数" prop="yynum">
      <el-input v-model="dataForm.yynum" placeholder="用印份数"></el-input>
    </el-form-item>
    <el-form-item label="用章类型" prop="type">
      <el-input v-model="dataForm.type" placeholder="用章类型"></el-input>
    </el-form-item>
    <el-form-item label="公司名称" prop="corpname">
      <el-input v-model="dataForm.corpname" placeholder="公司名称"></el-input>
    </el-form-item>
    <el-form-item label="文件名或用途" prop="fileormeno">
      <el-input v-model="dataForm.fileormeno" placeholder="文件名或用途"></el-input>
    </el-form-item>
    <el-form-item label="附件名称" prop="filename">
      <el-input v-model="dataForm.filename" placeholder="附件名称"></el-input>
    </el-form-item>
    <el-form-item label="附件id" prop="fileid">
      <el-input v-model="dataForm.fileid" placeholder="附件id"></el-input>
    </el-form-item>
    <el-form-item label="意见" prop="advice">
      <el-input v-model="dataForm.advice" placeholder="意见"></el-input>
    </el-form-item>
    <el-form-item label="抄送人" prop="mailcopier">
      <el-input v-model="dataForm.mailcopier" placeholder="抄送人"></el-input>
    </el-form-item>
    <el-form-item label="创建人" prop="creator">
      <el-input v-model="dataForm.creator" placeholder="创建人"></el-input>
    </el-form-item>
    <el-form-item label="创建时间" prop="creatdate">
      <el-input v-model="dataForm.creatdate" placeholder="创建时间"></el-input>
    </el-form-item>
    <el-form-item label="关联事件" prop="event">
      <el-input v-model="dataForm.event" placeholder="关联事件"></el-input>
    </el-form-item>
    <el-form-item label="关联项目" prop="project">
      <el-input v-model="dataForm.project" placeholder="关联项目"></el-input>
    </el-form-item>
    <el-form-item label="下一处理环节" prop="nextop">
      <el-input v-model="dataForm.nextop" placeholder="下一处理环节"></el-input>
    </el-form-item>
    <el-form-item label="下一处理人" prop="nextoper">
      <el-input v-model="dataForm.nextoper" placeholder="下一处理人"></el-input>
    </el-form-item>
    <el-form-item label="是否回执" prop="comeon">
      <el-input v-model="dataForm.comeon" placeholder="是否回执"></el-input>
    </el-form-item>
    <el-form-item label="推送流程状态" prop="appresult">
      <el-input v-model="dataForm.appresult" placeholder="推送流程状态"></el-input>
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
          appname: '',
          appdate: '',
          depart: '',
          yynum: '',
          type: '',
          corpname: '',
          fileormeno: '',
          filename: '',
          fileid: '',
          advice: '',
          mailcopier: '',
          creator: '',
          creatdate: '',
          event: '',
          project: '',
          nextop: '',
          nextoper: '',
          comeon: '',
          appresult: ''
        },
        dataRule: {
          appname: [
            { required: true, message: '起草人不能为空', trigger: 'blur' }
          ],
          appdate: [
            { required: true, message: '起草时间不能为空', trigger: 'blur' }
          ],
          depart: [
            { required: true, message: '所在部门不能为空', trigger: 'blur' }
          ],
          yynum: [
            { required: true, message: '用印份数不能为空', trigger: 'blur' }
          ],
          type: [
            { required: true, message: '用章类型不能为空', trigger: 'blur' }
          ],
          corpname: [
            { required: true, message: '公司名称不能为空', trigger: 'blur' }
          ],
          fileormeno: [
            { required: true, message: '文件名或用途不能为空', trigger: 'blur' }
          ],
          filename: [
            { required: true, message: '附件名称不能为空', trigger: 'blur' }
          ],
          fileid: [
            { required: true, message: '附件id不能为空', trigger: 'blur' }
          ],
          advice: [
            { required: true, message: '意见不能为空', trigger: 'blur' }
          ],
          mailcopier: [
            { required: true, message: '抄送人不能为空', trigger: 'blur' }
          ],
          creator: [
            { required: true, message: '创建人不能为空', trigger: 'blur' }
          ],
          creatdate: [
            { required: true, message: '创建时间不能为空', trigger: 'blur' }
          ],
          event: [
            { required: true, message: '关联事件不能为空', trigger: 'blur' }
          ],
          project: [
            { required: true, message: '关联项目不能为空', trigger: 'blur' }
          ],
          nextop: [
            { required: true, message: '下一处理环节不能为空', trigger: 'blur' }
          ],
          nextoper: [
            { required: true, message: '下一处理人不能为空', trigger: 'blur' }
          ],
          comeon: [
            { required: true, message: '是否回执不能为空', trigger: 'blur' }
          ],
          appresult: [
            { required: true, message: '推送流程状态不能为空', trigger: 'blur' }
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
              url: this.$http.adornUrl(`/oa/oayinzsq/info/${this.dataForm.id}`),
              method: 'get',
              params: this.$http.adornParams()
            }).then(({data}) => {
              if (data && data.code === 0) {
                this.dataForm.appname = data.oayinzsq.appname
                this.dataForm.appdate = data.oayinzsq.appdate
                this.dataForm.depart = data.oayinzsq.depart
                this.dataForm.yynum = data.oayinzsq.yynum
                this.dataForm.type = data.oayinzsq.type
                this.dataForm.corpname = data.oayinzsq.corpname
                this.dataForm.fileormeno = data.oayinzsq.fileormeno
                this.dataForm.filename = data.oayinzsq.filename
                this.dataForm.fileid = data.oayinzsq.fileid
                this.dataForm.advice = data.oayinzsq.advice
                this.dataForm.mailcopier = data.oayinzsq.mailcopier
                this.dataForm.creator = data.oayinzsq.creator
                this.dataForm.creatdate = data.oayinzsq.creatdate
                this.dataForm.event = data.oayinzsq.event
                this.dataForm.project = data.oayinzsq.project
                this.dataForm.nextop = data.oayinzsq.nextop
                this.dataForm.nextoper = data.oayinzsq.nextoper
                this.dataForm.comeon = data.oayinzsq.comeon
                this.dataForm.appresult = data.oayinzsq.appresult
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
              url: this.$http.adornUrl(`/oa/oayinzsq/${!this.dataForm.id ? 'save' : 'update'}`),
              method: 'post',
              data: this.$http.adornData({
                'id': this.dataForm.id || undefined,
                'appname': this.dataForm.appname,
                'appdate': this.dataForm.appdate,
                'depart': this.dataForm.depart,
                'yynum': this.dataForm.yynum,
                'type': this.dataForm.type,
                'corpname': this.dataForm.corpname,
                'fileormeno': this.dataForm.fileormeno,
                'filename': this.dataForm.filename,
                'fileid': this.dataForm.fileid,
                'advice': this.dataForm.advice,
                'mailcopier': this.dataForm.mailcopier,
                'creator': this.dataForm.creator,
                'creatdate': this.dataForm.creatdate,
                'event': this.dataForm.event,
                'project': this.dataForm.project,
                'nextop': this.dataForm.nextop,
                'nextoper': this.dataForm.nextoper,
                'comeon': this.dataForm.comeon,
                'appresult': this.dataForm.appresult
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
