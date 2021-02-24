<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png" />
    <postForm></postForm>
    <post v-for="post in posts" :key="post.id" :post="post"></post>
  </div>
</template>

<script>
import axios from "axios";
import post from "./components/post.vue";
import postForm from "./components/postForm.vue";

export default {
  name: "App",
  components: {
    post,
    postForm,
  },
  data() {
    return {
      posts: [],
    };
  },
  mounted() {
    axios
      .request({
        url: "http://127.0.0.1:5000/api/posts",
        method: "GET",
      })
      .then((response) => {
        this.posts = response.data;
      })
      .catch((err) => {
        console.log(err);
      });
    
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
