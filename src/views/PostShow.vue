<template>
  <div class="home">
    <h1>{{ post.title }}</h1>
    <img v-bind:src="post.image" alt="" />
    <p>{{ post.body }}</p>
    <button @click="deleteWarning()">Delete</button>
    |
    <router-link v-bind:to="`/posts/${post.id}/edit`">Edit Post</router-link>
    |
    <a href="/posts">Return to All Posts</a>

    <dialog id="delete-details">
      <form method="dialog">
        <h3>Are you sure you want to delete?</h3>
        <button @click="deletePost(post)">Yes</button>
        <button>Close</button>
      </form>
    </dialog>
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
    deleteWarning: function () {
      document.querySelector("#delete-details").showModal();
    },
    deletePost: function (post) {
      axios.delete(`/posts/${post.id}`).then((response) => {
        console.log("Post Successfully Deleted", response);
        this.$router.push("/posts");
      });
    },
  },
};
</script>
