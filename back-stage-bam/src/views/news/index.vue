<template>
  <div>
   <el-card>
     <el-table :data="tableData">
        <el-table-column label="新闻标题" prop="title"/>
        <el-table-column label="作者" prop="author.nickname"/>
        <el-table-column  label="新闻头图">
          <template slot-scope="scope"> 
            <img :src="scope.row.img"  class="table-item-img">
          </template>
        </el-table-column>
        <el-table-column label="分类" prop="type.title" />
        <el-table-column label="操作">
          <template slot-scope="scope">
            <el-button type="primary" size="mine">查看详细</el-button>
            <el-button type="danger" size="mine">删除</el-button>
          </template>
        </el-table-column>
      </el-table>
   </el-card>
  </div>
</template>

<script>
  export default {
    data(){
      return{
        tableData:[]
      }
    },
    methods:{
      getData(){
        this.$axios.get('/admin/news').then(res=>{
          console.log(res)
            this.tableData = res.data
        })
      }
    },
    created(){
      this.getData()
    }
  }
</script>

<style scoped>

</style>