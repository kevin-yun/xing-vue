<template>
  <div>
    <i class="el-icon-circle-plus-outline" @click="dialogFormVisible = true"></i>
    <el-dialog
      title="添加/修改图书"
      :visible.sync="dialogFormVisible"
      @close="clear">
      <el-form v-model="form" style="text-align: left" ref="dataForm">
        <el-form-item label="书名" :label-width="formLabelWidth" prop="title">
          <el-input v-model="form.title" autocomplete="off" placeholder="不加《》"></el-input>
        </el-form-item>
        <el-form-item label="作者" :label-width="formLabelWidth" prop="author">
          <el-input v-model="form.author" autocomplete="off"></el-input>
        </el-form-item>
        <el-form-item label="出版日期" :label-width="formLabelWidth" prop="publicationDate">
          <el-input v-model="form.publicationDate" autocomplete="off"></el-input>
        </el-form-item>
        <el-form-item label="出版社" :label-width="formLabelWidth" prop="press">
          <el-input v-model="form.press" autocomplete="off"></el-input>
        </el-form-item>
        <el-form-item label="封面" :label-width="formLabelWidth" prop="coverUrl">
          <el-input v-model="form.coverUrl" autocomplete="off" placeholder="图片 URL"></el-input>
        </el-form-item>
        <el-form-item label="简介" :label-width="formLabelWidth" prop="abs">
          <el-input type="textarea" v-model="form.abs" autocomplete="off"></el-input>
        </el-form-item>
        <el-form-item label="分类" :label-width="formLabelWidth" prop="categoryId">
          <el-select v-model="form.categoryId" placeholder="请选择分类">
            <el-option v-for="item of form.categoryArr" :key="item.id" :label="item.name" :value="item.id"></el-option>
          </el-select>
        </el-form-item>
        <el-form-item prop="id" style="height: 0">
          <el-input type="hidden" v-model="form.id" autocomplete="off"></el-input>
        </el-form-item>
      </el-form>
      <div slot="footer" class="dialog-footer">
        <el-button @click="dialogFormVisible = false">取 消</el-button>
        <el-button type="primary" @click="onSubmit">确 定</el-button>
      </div>
    </el-dialog>
  </div>
</template>

<script>
export default {
  name: 'EditForm',
  data () {
    return {
      dialogFormVisible: false,
      form: {
        id: '',
        title: '',
        author: '',
        publicationDate: '',
        press: '',
        coverUrl: '',
        abs: '',
        categoryId: '',
        categoryArr: []
      },
      formLabelWidth: '120px'
    }
  },
  methods: {
    clear () {
      this.form = {
        id: '',
        title: '',
        author: '',
        publicationDate: '',
        press: '',
        coverUrl: '',
        abs: '',
        categoryId: ''
      }
    },
    onSubmit () {
      this.$axios.post('/book/add', {
        id: this.form.id,
        coverUrl: this.form.coverUrl,
        title: this.form.title,
        author: this.form.author,
        publicationDate: this.form.publicationDate,
        press: this.form.press,
        abs: this.form.abs,
        categoryId: this.form.categoryId
      }).then(resp => {
        if (resp && resp.status === 200) {
          this.dialogFormVisible = false
          this.$emit('onSubmit')
        }
      })
    }
  }
}
</script>

<style scoped>
  .el-icon-circle-plus-outline {
    margin: 50px 0 0 20px;
    font-size: 100px;
    float: left;
    cursor: pointer;
  }
</style>
