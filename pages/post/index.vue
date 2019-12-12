<template>
  <section class="container">
    <!-- 侧边栏 -->
    <div class="aside">
      <!-- 城市列表 -->
      <cities @click="handlerHot" />
    </div>
    <div class="main">
      <postHeader @search="handlersearch" :searchCity="city" />
      <PostList
        :article="item"
        v-for="(item,index) in dataList"
        :key="index"
        @clickPost="$router.push({path:`/post/detail?id=${item.id}`})"
        @clickWriter="$router.push({path:`user/personal`})"
      />
      <el-pagination
        @size-change="handleSizeChange"
        @current-change="handleCurrentChange"
        :current-page="pageIndex"
        :page-sizes="[3, 5, 10,15]"
        :page-size="pageSize"
        layout="total, sizes, prev, pager, next, jumper"
        :total="postsList.length"
      ></el-pagination>
    </div>
  </section>
</template>

<script>
import cities from "@/components/post/cities";
import postHeader from "@/components/post/postHeader";
import PostList from "@/components/post/PostList";

export default {
  data() {
    return {
      postsList: "",
      pageSize: 3,
      pageIndex: 1,
      city: "广州"
    };
  },
  components: {
    cities,
    postHeader,
    PostList
  },
  computed: {
    dataList() {
      const start = (this.pageIndex - 1) * this.pageSize;
      const end = start + this.pageSize;
      return this.postsList.slice(start, end);
    }
  },
  mounted() {
    this.$axios({
      url: "/posts"
    }).then(res => {
      // console.log(res.data.data);
      this.postsList = res.data.data;
    });
  },
  methods: {
    handleSizeChange(pageSize) {
      this.pageIndex = 1;
      this.pageSize = pageSize;
    },
    handleCurrentChange(pageIndex) {
      this.pageIndex = pageIndex;
    },
    handlerHot(val) {
      this.city = val;
      this.$axios({
        url: "/posts",
        params: {
          city: this.city
        }
      }).then(res => {
        this.postsList = res.data.data;
        this.pageIndex = 1;
      });
    },
    handlersearch(val) {
      console.log(val);
      this.postsList = val;
      this.pageIndex = 1;
    }
  }
};
</script>

<style scoped lang="less">
.container {
  width: 1000px;
  margin: 0 auto;
  padding: 20px 0;
  display: flex;
  .aside {
    flex: 3;
  }
  .main {
    flex: 7;
  }
}
</style>