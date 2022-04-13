<script>
import axios from "axios";
export default {
  data: function () {
    return {
      message: "Create new posts here:",
      post: {},
      newPost: {},
      errors: [],
    };
  },
  created: function () {
    this.showPosts();
    // this.destroyPost();
  },
  methods: {
    showPosts() {
      axios.get(`/posts/${this.$route.params.id}`).then((response) => {
        this.post = response.data;
      });
    },
    destroyPost() {
      axios.delete(`/posts/${this.newPost.id}`).then((response) => {
        console.log(response);
        this.$router.push("/posts");
      });
    },
  },
};
</script>

<template>
  <div class="home">
    <h1>Post Info</h1>
    <p>Title: {{ post.title }}</p>
    <p>Body: {{ post.body }}</p>
    <router-link v-bind:to="`/posts/${post.id}`">
      <img v-bind:src="post.image" v-bind:alt="post.name" />
    </router-link>
    <router-link to="/posts" style="margin-right: 10px">Back to Posts</router-link>
    <router-link v-bind:to="`/posts/${post.id}/edit`" style="margin-right: 10px">Edit Post</router-link>
    <button v-on:click="destroyPost">Delete</button>
  </div>
</template>
