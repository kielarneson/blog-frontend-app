<template>
  <div class="editPost">
    <form v-on:submit.prevent="updatePost(post)">
      <h1>Edit Post</h1>
      <ul>
        <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
      </ul>
      <div>
        <label>Title:</label>
        <input type="text" v-model="post.title" />
      </div>
      <div>
        <label>Body:</label>
        <input type="text" v-model="post.body" />
      </div>
      <div>
        <label>Image URL:</label>
        <input type="text" v-model="post.image" />
      </div>
      <input type="submit" value="submit" />
      |
      <router-link to="/posts">Cancel</router-link>
    </form>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      post: {},
      editPostParams: {},
      errors: [],
    };
  },
  created: function () {
    axios.get(`/posts/${this.$route.params.id}`).then((response) => {
      this.post = response.data;
    });
  },
  methods: {
    updatePost: function (post) {
      var editPostParams = post;
      axios
        .patch(`/posts/${this.post.id}`, editPostParams)
        .then((response) => {
          console.log(response.data);
          this.$router.push("/posts");
        })
        .catch((error) => {
          this.errors = error.response.data.errors;
        });
    },
  },
};
</script>
