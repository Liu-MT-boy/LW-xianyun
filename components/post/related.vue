<template>
  <div class="aside">
    <h4 class="aside-title">相关攻略</h4>
    <div class="recommend-list" v-for="(item,index) in recommend" :key="index">
      <a :href="`/post/detail?id=${item.id}`" class="recommend-item">
        <div class="post-imgText el-row el-row--flex">
          <div class="post-img el-row is-align-middle el-row--flex">
            <img :src="item.images[0]" alt />
          </div>
          <div class="post-text">
            <div>{{item.title}}</div>
            <p>{{item.created_at}} 阅读 {{item.watch}}</p>
          </div>
        </div>
      </a>
    </div>
  </div>
</template>

<script>
import moment from 'moment'
export default {
  data() {
    return {
      recommend: ""
    };
  },
  mounted() {
    this.$axios({
      url: "posts/recommend"
    }).then(res => {
      // this.recommend=res.data.data
      // console.log(this.recommend);
      this.recommend = res.data.data.map(value => {
        let data = new Date(value.created_at);
        let year = data.getFullYear();
        let month = data.getMonth() + 1;
        let day = data.getDate();
        let hour = data.getHours();
        let min = data.getMinutes();
        let time = year + "-" + month + "-" + day + " " + hour + ":" + min
        return {
          ...value,
          created_at: time
        };
      });
      console.log(this.recommend);
    });
  }
};
</script>

<style lang="less">
* {
  margin: 0;
  padding: 0;
}
.aside {
  width: 280px;
}
.aside-title {
  font-weight: 400;
  font-size: 18px;
  padding-bottom: 10px;
  border-bottom: 1px solid #ddd;
}
.recommend-item {
  display: block;
  padding: 20px 0;
  border-bottom: 1px solid #ddd;
}
.el-row--flex {
  display: flex;
}
.el-row {
  box-sizing: border-box;
}
.aside .recommend-item .post-imgText .post-img {
  width: 100px;
  height: 80px;
  flex-shrink: 0;
  background: #ddd;
  overflow: hidden;
  margin-right: 10px;
}
.el-row--flex.is-align-middle {
  align-items: center;
}
.aside .recommend-item .post-imgText .post-img img {
  width: 100%;
  height: 100%;
  -o-object-fit: cover;
  object-fit: cover;
}
.aside .recommend-item .post-imgText .post-text {
  flex: 1;
  position: relative;
}
.aside .recommend-item .post-imgText .post-text div {
  position: relative;
  line-height: 1.4em;
  height: 2.8em;
  overflow: hidden;
  position: absolute;
  left: 0;
  top: 0;
  width: 100%;
}
.aside .recommend-item .post-imgText .post-text p {
  position: absolute;
  bottom: 0;
  left: 0;
  font-size: 12px;
  color: #999;
}
</style>