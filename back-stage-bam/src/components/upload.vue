<template>
  <el-upload
  class="avatar-uploader"
  action="https://upload-z1.qiniup.com"
  :show-file-list="false"
  :on-success="handlSuccess"
  :data="formData"
  >
  <img v-if="imageUrl" :src="imageUrl" class="avatar">
  <i v-else class="el-icon-plus avatar-uploader-icon"></i>
</el-upload>
</template>

<script>
import axios from 'axios'
  export default {
     props:{
        value:String
      },
    data(){
      
      return{
        formData:{
          token:''
        },
        imageUrl:this.value
      }
    },
    methods:{
      getToken(){
        axios.get('http://upload.yaojunrong.com/getToken').then(res=>{
            this.formData.token = res.data.data
        })
      },
      handlSuccess(res){
        this.imageUrl = res.url
        this.$emit('input',this.imageUrl)
      }
    },
    created(){
      this.getToken()
    },
    watch:{
      value(val){
        this.imageUrl = val
      }
    }
  }
</script>

<style scoped>
  .avatar-uploader .el-upload {
    border-radius: 6px;
    cursor: pointer;
    position: relative;
    overflow: hidden;
  }
  .avatar-uploader .el-upload:hover {
    border-color: #409EFF;
  }
  .avatar-uploader-icon {
    border: 1px dashed #666;
    font-size: 28px;
    color: #8c939d;
    width: 178px;
    height: 178px;
    line-height: 178px;
    text-align: center;
  }
  .avatar {
    width: 178px;
    height: 178px;
    display: block;
  }
</style>