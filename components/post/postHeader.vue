<template>
  <div class="header">
    <div class="search">
      <input
        type="text"
        placeholder="请输入想去的地方，比如：'广州'"
        v-model="searchCity"
        @keyup.enter="search"
      />
      <strong class="el-icon-search" @click="search"></strong>
    </div>
    <div class="recommend">
      推荐:&nbsp;&nbsp;
      <span @click="recommend('广州')">广州</span>
      <span @click="recommend('上海')">上海</span>
      <span @click="recommend('北京')">北京</span>
    </div>
    <div class="post-head">
      <span class="word">推荐攻略</span>
      <button>
        <i class="el-icon-edit"></i>
        <span>写游记</span>
      </button>
    </div>
  </div>
</template>

<script>
export default {
  props: ['searchCity'],
  data() {
    return {
      posts:''
    };
  },
  methods: {
    search() {
      if(this.searchCity){
        this.$axios({
          url:'/posts',
          params:{
            city:this.searchCity
          }
        }).then(res=>{
          this.posts=res.data.data
          this.$emit('search',this.posts)
        }) 
      }
    },
    recommend(val){
      this.searchCity=val
      this.$axios({
          url:'/posts',
          params:{
            city:val
          }
        }).then(res=>{
          this.posts=res.data.data
          this.$emit('search',this.posts)
        }) 
    }
  }
};
</script>

<style scoped lang="less">
.search {
  width: 700px;
  border: 3px solid #ffa500;
  input {
    width: 655px;
    height: 34px;
    padding: 0 20px;
    border: none;
    outline: none;
  }
  .el-icon-search {
    float: right;
    padding-top: 5px;
    margin-right: 10px;
    font-weight: 900;
    font-size: 24px;
    color: #ffa500;
    cursor: pointer;
  }
}
.recommend {
  padding: 10px 0;
  font-size: 12px;
  color: #666;
  span {
    margin-right: 5px;
    &:hover{
      cursor: pointer;
      color: orange
    }
  }
}
.post-head {
  width: 700px;
  height: 51px;
  line-height: 40px;
  padding-bottom: 10px;
  border-bottom: 1px solid #ccc;
  .word {
    float: left;
    height: 51px;
    width: 74px;
    font-size: 18px;
    color: #ffa500;
    border-bottom: 2px solid #ffa500;
  }
  button {
    float: right;
    width: 107px;
    height: 40px;
    background: #409eff;
    border: none;
    border-radius: 4px;
    outline: none;
    text-align: center;
    font-size: 14px;
    color: #fff;
    span {
      margin-left: 5px;
    }
    &:hover {
      cursor: pointer;
      background: #66b1ff;
    }
  }
}
</style>