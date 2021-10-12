<template>
  <div class="postIndex">
    <h1>All Posts</h1>
    <div>
      Search:
      <input type="text" v-model="searchFilter" />
    </div>
    <div class="row">
      <div class="col-sm-4" v-for="post in filterBy(posts, searchFilter, 'title', 'description')" v-bind:key="post.id">
        <div class="card text-center">
          <div class="card-body">
            <h5 class="card-title">{{ post.title }}</h5>
            <img :src="post.image" alt="" />
            <div>
              <router-link v-bind:to="`/posts/${post.id}`">Show More</router-link>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style>
.card img {
  object-fit: cover;
  height: 400px;
}

img {
  width: 300px;
}

h1 {
  text-align: center;
  padding-top: 15px;
}
</style>

<script>
import axios from "axios";
import Vue2Filters from "vue2-filters";

export default {
  mixins: [Vue2Filters.mixin],
  data: function () {
    return {
      posts: [],
      searchFilter: "",
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
