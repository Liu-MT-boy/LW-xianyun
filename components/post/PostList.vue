<template>
  <div class="article" v-if="article.images.length <= 1">
    <img :src="article.images[0]" alt class="img" @click="handlerclick" />
    <div class="container">
      <p class="title" @click="handlerclick">{{article.title}}</p>
      <div class="text" v-html="article.summary" @click="handlerclick"></div>
      <div class="message">
        <span class="cityname">
          <i class="el-icon-location-outline"></i>
          {{article.city.name}}
        </span>
        <div class="writer">
          by
          <img src="http://157.122.54.189:9095/assets/images/avatar.jpg" alt />
          <span class="writerName" @click="handlerWriter">{{article.account.nickname}}</span>
        </div>
        <span class="watch">
          <i class="el-icon-view"></i>
          {{article.watch}}
        </span>
        <span class="like">{{article.like}}赞</span>
      </div>
    </div>
  </div>
  <div class="article" v-else-if="article.images.length = 3">
    <div class="container">
      <p class="title" @click="handlerclick">{{article.title}}</p>
      <div class="text" v-html="article.summary" @click="handlerclick"></div>
      <div class="pictures">
        <img :src="article.images[0]" alt class="imgs" @click="handlerclick" />
        <img :src="article.images[1]" alt class="imgs" @click="handlerclick" />
        <img :src="article.images[2]" alt class="imgs" @click="handlerclick" />
      </div>
      <div class="message">
        <span class="cityname">
          <i class="el-icon-location-outline"></i>
          {{article.city.name}}
        </span>
        <div class="writer">
          by
          <img src="http://157.122.54.189:9095/assets/images/avatar.jpg" alt />
          <span class="writerName" @click="handlerWriter">{{article.account.nickname}}</span>
        </div>
        <span class="watch">
          <i class="el-icon-view"></i>
          {{article.watch}}
        </span>
        <span class="like">{{article.like}}赞</span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ["article"],
  data() {
    return {};
  },
  methods: {
    handlerclick(event) {
      this.$emit("clickPost", event);
    },
    handlerWriter(event) {
      this.$emit("clickWriter", event);
    }
  }
};
</script>

<style scoped lang="less">
.article {
  width: 700px;
  display: flex;
  padding: 20px 0;
  .img {
    float: left;
    margin-right: 8px;
    width: 220px;
    height: 150px;
    &:hover {
      cursor: pointer;
    }
  }
  .pictures {
    display: flex;
    justify-content: space-between;
    .imgs {
      width: 220px;
      height: 150px;
      &:hover {
        cursor: pointer;
      }
    }
  }
  .container {
    overflow: hidden;
    .title {
      height: 39px;
      font-size: 18px;
      white-space: nowrap;
      text-overflow: ellipsis;
      overflow: hidden;
      margin-bottom: 15px;
      &:hover {
        color: orange;
        cursor: pointer;
      }
    }
    .text {
      margin-bottom: 15px;
      line-height: 1.5;
      font-size: 14px;
      height: 63px;
      overflow: hidden;
      text-overflow: ellipsis;
      display: -webkit-box;
      -webkit-line-clamp: 3;
      &:hover {
        cursor: pointer;
      }
    }
    .message {
      display: flex;
      line-height: 26px;
      font-size: 12px;
      color: #999;
      .cityname {
        margin-right: 10px;
      }
      .writer {
        margin-right: 10px;
        img {
          vertical-align: middle;
          width: 16px;
          height: 16px;
          border-radius: 8px;
          margin: 5px;
        }
        .writerName {
          color: orange;
          &:hover {
            cursor: pointer;
          }
        }
      }
      .watch {
        flex: 1;
      }
      .like {
        font-size: 16px;
        color: orange;
      }
    }
  }
}
</style>