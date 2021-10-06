<template>
  <div class="postIndex">
    <h1>All Posts</h1>
    <div v-for="post in posts" v-bind:key="post.id">
      <a v-bind:href="`/posts/${post.id}`">
        <img :src="post.image" alt="" />
      </a>
    </div>
  </div>
</template>

<style>
p {
  padding-left: 100px;
  padding-right: 100px;
}
</style>

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      posts: [],
    };
  },
  created: function () {
    this.indexPosts();
  },
  methods: {
    indexPosts: function () {
      axios.get("/posts").then((response) => {
        console.log(response.data);
        this.posts = response.data;
      });
    },
  },
};
</script>
