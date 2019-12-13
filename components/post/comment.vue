<template>
  <el-row>
    <el-col :span="24">
    <div class="commentList">
      <div class="item">
        <div class="head">
          <img src="" alt />
          <div>
            <span>火星网友</span>
            <span>2小时前</span>
          </div>
        </div>
        <div class="text">文章说得很有道理</div>
        <img src="" alt />
      </div>
    </div>
    </el-col>
    <el-col :span="24">
    <el-pagination
      @size-change="handleSizeChange"
      @current-change="handleCurrentChange"
      :current-page="pageIndex"
      :page-sizes="[2, 4, 6, 8]"
      :page-size="2"
      layout="total, sizes, prev, pager, next, jumper"
      :total="total">
    </el-pagination>
     </el-col>
      </el-row>
    </template>

<script>
export default {
  data () {
    return {
      reviewdata : ""
    }
  },
  mounted () {
    this.$axios({
      url: `/posts/comments`,
      params: {
        post:`this.$route.id`
      }
    }).then(res => {
      console.log(res);
      this.reviewdata=res.data
      console.log(res.data);
    //   console.log(this.contain);
    });
   console.log(this.$route.query.id);
  }
  }
</script>

<style lang='less' scoped>
.commentList{
    border: 1px solid #ccc;
    border-bottom: 2px dashed #ddd;
    padding: 5px 20px 5px;
}
.head{
  margin-bottom: 10px;
  font-size: 12px;
  color: #666;
}
.img {
   height:10px;
   width:10px;
}
</style>