<template>
<div class="largeFrame">
  <div class="userComment" v-for="(item, index) in commentsList" :key="index">
    <commentRecursion :data='item'></commentRecursion>
  </div>
</div>
</template>

<script>
import commentRecursion from '~/components/post/commentRecursion'
export default {
  name:"UserList",
  props: ["postid","pageIndex","pageSize"],
  components: {
    commentRecursion
  },
  data() {
    return {
        commentsList:{
        },
        recommentsList:[]
    }
  },
  watch: {
      pageIndex() {
          this.getDate()
      },
      pageSize(){
          this.getDate()
      }
  },
  methods: {
      getDate () {
           this.$axios({
                url:'/posts/comments',
                data:this.postid
            }).then(res => {
               let arr = res.data.data.map(value => {
                const data = new Date (value.created_at*1)
                    let year = data.getFullYear()
                    let month = data.getMonth() + 1
                    let day = data.getDate()
                    let time = year + "-" + month + "-" + day
                    return {
                        ...value,
                        created_at: time
                    }
                })
                console.log(arr);
                arr.forEach( item => {
                    if(item.parent){
                        this.recommentsList.push(item.parent)
                    }
                })
                console.log(this.pageIndex,this.pageSize);
                let star  = (this.pageIndex - 1) * this.pageSize
                 let end =  star  + this.pageSize 
                 this.commentsList = arr.slice(star,end)
                
            })
      }
  },
  mounted() {
       this.getDate()    
  }
};
</script>

<style lang="less" scoped>
.userComment {
  &:hover{
      >span{
          display: block;
      }
  }
     > span {
        position: absolute;
        font-size: 12px;
        line-height: 20px;
        color: #6475c1;
        display: none;
        bottom: 0;
        right: 10px;
        &:hover {
          text-decoration: underline;
          cursor: pointer;
        }
      }
  .comment {
    .name {
      display: flex;
      justify-content: space-between;
      span {
        font-size: 14px;
        color: #666;
      }
      span:nth-child(3) {
        color: #999;
      }
    }
    .user {
      display: flex;
      .user_img {
        display: block;
        width: 16px;
        height: 16px;
      }
    }
    .content-img {
      width: 100%;
      position: relative;
      justify-content: space-between;
      > p {
        text-align: left;
        padding-left: 25px;
        font-size: 14px;
      }
      .img {
        padding:10px 10px 20px 0;
        padding-left: 15px;
        display: flex;
       >div{
           width:80px;
          height: 80px;
           padding: 5px;
           margin-right: 10px;
           border: dashed 1px #999;
            img {
           width:80px;
          height: 80px;
          background-size: cover;
          text-align: left;
        }
       }
       
      }
    }
  }
}
</style>
