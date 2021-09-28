<template>
  <el-container>
    <el-aside style="width: 200px;margin-top: 20px">
      <switch></switch>
      <SideMenu @indexSelect="listByCategory" ref="sideMenu"></SideMenu>
    </el-aside>
    <el-main>
      <books class="books-area" ref="booksArea"></books>
    </el-main>
  </el-container>
</template>

<script>
import SideMenu from './SideMenu'
import Books from './Books'

export default {
  name: 'AppLibrary',
  components: {Books, SideMenu},
  mounted: function () {
    this.loadCategoryList()
  },
  methods: {
    loadCategoryList () {
      const _this = this
      this.$axios.get('/category/findList').then(resp => {
        if (resp && resp.status === 200) {
          const obj = JSON.parse(JSON.stringify(resp.data))
          _this.$refs.sideMenu.category_arr = obj.data
          _this.$refs.booksArea.$refs.edit.categoryArr = obj.data
        }
      })
    },
    listByCategory () {
      var _this = this
      this.$axios.post('/book/findListByCategoryId', {
        categoryId: this.$refs.sideMenu.cid
      }).then(resp => {
        if (resp && resp.status === 200) {
          _this.$refs.booksArea.books = JSON.parse(JSON.stringify(resp.data)).data
        }
      })
    }
  }
}
</script>

<style scoped>
  .books-area {
    width: 990px;
    margin-left: auto;
    margin-right: auto;
  }
</style>
