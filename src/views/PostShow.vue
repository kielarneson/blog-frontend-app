<template>
  <div class="home">
    <h1>{{ post.title }}</h1>
    <img v-bind:src="post.image" alt="" />
    <p>{{ post.body }}</p>
    <router-link v-bind:to="`/posts/${post.id}/edit`">Edit Post</router-link>
    |
    <a href="/posts">Return to All Posts</a>
  </div>
</template>

<style></style>

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      post: {},
    };
  },
  created: function () {
    this.showPost();
  },
  methods: {
    showPost: function () {
      axios.get(`/posts/${this.$route.params.id}`).then((response) => {
        this.post = response.data;
      });
    },
  },
};
</script>
