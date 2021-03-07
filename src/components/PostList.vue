<template>
  <div>
    <div v-if="isLoading">
      <img src="../assets/loading.gif">
    </div>
    <div>
      <ul>
        <li v-for="post in posts" :key="post.id">
          <img src="post.ava" alt="">
        </li>
      </ul>
    </div>
  </div>

</template>

<script>
import Vue from 'vue'
import axios from 'axios'
Vue.prototype.$http = axios
export default {
    data(){
      return {
        isLoading: false,
        posts:[]
      }
    },
    methods: {
      getData(){
        this.$http.get('https://cnodejs.org/api/v1/topics', {
          params:{
            limit: 20,
            page: 1
          }
        })
        .then((res)=>{
          this.isLoading = false
          this.posts = res.data.data
        })
        .catch((err)=>{
          console.log(err)
        })
      }
    },
  beforeMount(){
      this.isLoading = true
      this.getData()
  }
}
</script>

<style scoped>

</style>