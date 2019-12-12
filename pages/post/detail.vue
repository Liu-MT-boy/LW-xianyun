<template>
  <div class="container">
    <!--文章部分-->
    <div class="main">
      <!-- 面包屑 -->
      <el-breadcrumb separator="/">
        <el-breadcrumb-item :to="{ path: '/post' }">旅游攻略</el-breadcrumb-item>
        <el-breadcrumb-item>攻略详情</el-breadcrumb-item>
      </el-breadcrumb>
      <div class="post-content">
        <el-row>
          <el-col :span="24">
            <div class="grid-content bg-purple-dark"><h1>{{contain.title}}</h1></div>
          </el-col>
        </el-row>
        <el-row>
          <el-col :span="24">
            <div class="grid-content bg-purple-dark gonglue">
                <span>攻略:</span>
                <span>阅读：{{contain.watch}}</span>
            </div>
          </el-col>
        </el-row>
        <el-row>
          <el-col :span="24">
            <div class="grid-content bg-purple-dark" v-html="contain.content"></div>
          </el-col>
        </el-row>
        <div class="post-ctrl">
        <div class="el-row is-justify-center el-row--flex">
          <div class="ctrl-item" @click="handelFocus">
            <i class="iconfont iconpinglun"></i>
            <p>评论(100)</p>
          </div>
          <div class="ctrl-item">
            <i class="iconfont iconstar1"></i>
            <p>收藏</p>
          </div>
          <div class="ctrl-item">
            <i class="iconfont iconfenxiang"></i>
            <p>分享</p>
          </div>
          <div class="ctrl-item">
            <i class="iconfont iconding"></i>
            <p>点赞(68)</p>
          </div>
        </div>
      </div>
         <el-input
            type="textarea"
            :rows="2"
            ref="comit"
            placeholder="说点什么吧..."
            resize="none">
          </el-input>
      </div>
      <!-- 评论区 -->
      <Comment />
    </div>

    <!-- 相关攻略 -->
    <Related />
  </div>
</template>

<script>
import Related from "@/components/post/related";
import Comment from "@/components/post/comment";
export default {
  components: {
    Related,
    Comment
  },
  data() {
    return {
        contain:"",
        commetn:''
    };
  },
  methods: {
    handelFocus(){
      console.log(123);
      this.commetn = true
      this.$refs.comit.focus()
    }
  },
  mounted() {
    this.$axios({
      url: `/posts/${this.$route.query.id}`
    }).then(res => {
      this.contain=res.data
    //   console.log(this.contain);
    });
   console.log(this.$route.query.id);
  }
};
</script>

<style>
.container {
  width: 1000px;
  margin: 0 auto;
  padding-top: 20px;
  display: flex;
  justify-content: space-between;
}
.main {
  width: 700px;
}
.main h1 {
  padding: 20px 0;
  border-bottom: 1px solid #ddd;
}
.main .post-info span {
  margin-left: 20px;
}
.main .post-ctrl {
  padding: 50px 0 30px;
}
.el-row--flex.is-justify-center {
  justify-content: center;
}
.el-row--flex {
  display: flex;
}
.el-row {
  box-sizing: border-box;
}
.main .post-ctrl .ctrl-item {
  margin: 0 20px;
  font-size: 20px;
  text-align: center;
  cursor: pointer;
}

.main .post-ctrl .ctrl-item i {
  display: block;
  font-size: 28px;
  color: orange;
}
.main .post-ctrl .ctrl-item:nth-child(2) i {
  -webkit-transform: scale(1.4);
  transform: scale(1.4);
}
.main .post-ctrl .ctrl-item p {
  margin-top: 5px;
  font-size: 14px;
  color: #999;
}
.main .cmt-title {
  font-weight: 400;
  font-size: 18px;
  margin-bottom: 20px;
}

.grid-content /deep/ img {
    max-width: 100%;
}
.gonglue{
    color:#999;
    padding : 20px;
    text-align: right;
}
</style>