<template>
  <div class="aside">
  <div class="menus" @mouseleave="sub=false">
    <div  v-for="(item,index) in menus" :key="index">
      <div @mouseover="sub=index" class="menus-item">
        <span class="text">{{item.type}}</span>
        <i class="el-icon-arrow-right"></i>
      </div>
      <div class="sub-menus" v-if="sub===index?true:false"> 
          <div class='text2' v-for="(item2,index2) in item.children" :key="index2" @click='handlerclick(item2.city)'>
            <i class="num">{{index2+1}}</i>
            <strong class="city">{{item2.city}}</strong>
            <span class="desc">{{item2.desc}}</span>
          </div>
      </div>
    </div>
  </div>
  <div class='recommend'>
    <p>
      推荐城市
    </p>
    <img src="https://dss3.bdstatic.com/70cFv8Sh_Q1YnxGkpoWK1HF6hhy/it/u=2695973191,2755975722&fm=26&gp=0.jpg" alt="" @click="handlerclick(null)"> 
  </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      menus: "",
      submenus: "",
      sub:'999'
    };
  },
  mounted() {
    this.$axios({
      url: "/posts/cities"
    }).then(res => {
      console.log(res);
      this.menus = res.data.data;
    });
  },
  methods: {
    handlerclick(val){
      this.$emit('click',val)
    }
  }
};
</script>

<style scoped lang="less">
.aside{
    width: 260px;
.menus {
  position: relative;
  border-left:1px solid #ddd;
   border-bottom: 1px solid #ddd;
  .menus-item {
    background-color: #fff;
    position: relative;
    z-index:2;
    width: 260px;
    height: 41px;
    line-height: 40px;
    padding: 0 12px 0 20px;
    border-top: 1px solid #ddd;
    box-sizing: border-box;
    border-right: 1px solid #ddd;
    font-size: 14px;
    &:hover{
      color: #FFA500;
      border-right: 1px solid #fff;
    }
    .el-icon-arrow-right {
      float: right;
      padding-top: 13px;
      font-size: 20px;
      color: #ccc
    }
  }
   .sub-menus {
      padding: 10px 20px;
      background-color: #fff;
      border: 1px solid #ccc;
      position: absolute;
      z-index: 1;
      top: 0;
      left: 259px;
      .text2{
        width: 350px;
        height: 34px;
        line-height: 34px;
        &:hover{
          cursor: pointer;
        }
        i{
          font-size: 24px;
          color: #FFA500
        }
        strong{
          font-size: 14px;
          color: #FFA500;
          margin: 0 10px
        }
        span{
          font-size: 14px;
          color:#999
        }
      }
    }
}
.recommend{
  margin-top: 20px;
  p{
    font-size: 16px;
    padding-bottom: 10px;
    margin-bottom: 10px;
    border-bottom:1px solid #ccc
  }
  img{
    width: 260px;
    cursor: pointer;
  }
}
}
</style>