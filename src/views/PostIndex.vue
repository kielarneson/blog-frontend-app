<template>
  <div class="postIndex">
    <h1>All Posts</h1>
    <div class="index" v-for="post in posts" v-bind:key="post.id">
      <h1>{{ post.title }}</h1>
      <img :src="post.image" alt="" />
      <div>
        <a v-bind:href="`/posts/${post.id}`">Show More</a>
      </div>
    </div>
  </div>
</template>

<style></style>

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
