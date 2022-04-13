<script>
import axios from "axios";
export default {
  data: function () {
    return {
      posts: [],
      currentPost: {},
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

    <div
      v-for="post in posts"
      v-bind:key="post.id"
      v-bind:class="{ selected: post === currentPost }"
      v-on:mouseover="currentPost = post"
      class="col"
    >
      <div class="card" style="width: 18rem">
        <img v-bind:src="post.image" class="card-img-top" v-bind:alt="post.name" />
        <div class="card-body">
          <h5 class="card-title">{{ post.title }}</h5>
          <p class="card-text">
            {{ post.body }}
          </p>
          <a v-bind:href="`/posts/${post.id}`">More Info</a>
        </div>
      </div>
      <h2>{{ post.name }}</h2>
    </div>
  </div>
</template>

<style>
.selected .card-body {
  color: white;
  background-color: rgb(43, 43, 43);
}
</style>
