<template>
<div class="article">
  <div class="loading" v-if="isLoading">
    <img src="../assets/loading.gif" alt="加载">
  </div>
  <div v-else>
    <div class="topic_header">
      <div class="topic_title">{{post.title}}</div>
      <ul>
        <li>•发布于：{{post.create_at | formatDate}}</li>
        <li>•作者：{{post.author.loginname}}</li>
        <li>•{{post.visit_count}}次浏览</li>
        <li>•来自{{post | tabFormatter}}</li>
      </ul>
      <div v-html="post.content" class="topic_content"></div>
    </div>

  </div>
</div>
</template>

<script>
export default {
  name: 'Article',
  data(){
    return {
      isLoading: false,
      post: {}
    }
  },
  methods:{
    getData(){
      this.$http.get(`https://cnodejs.org/api/v1/topic/${this.$route.params.id}`)
      .then(res=>{
        this.isLoading = false
        if(res.data.success){
          this.post = res.data.data
        }
      })
      .catch()
    }
  },
  beforeMount() {
    this.isLoading = true
    this.getData()
  }
}
</script>

<style>
@import "../assets/markdown-github.css";

</style>