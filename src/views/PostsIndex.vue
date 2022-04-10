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
        console.log("posts index", response);
        this.posts = response.data;
      });
    },
  },
};
</script>
<template>
  <div class="posts-index">
    <h1>Read the Things Here</h1>
    <div v-for="post in posts" v-bind:key="post.id">
      <h2>{{ post.name }}</h2>
      <img v-bind:src="post.url" v-bind:alt="post.name" />
      <h2>{{ post.title }}</h2>
      <p>{{ post.body }}</p>
      <p>{{ post.image }}</p>
    </div>
  </div>
</template>
