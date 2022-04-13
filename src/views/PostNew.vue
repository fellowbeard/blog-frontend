<script>
import axios from "axios";
export default {
  data: function () {
    return {
      message: "Create new posts here:",
      posts: [],
      newPost: {},
      errors: [],
    };
  },
  methods: {
    createPost() {
      axios
        .post("/posts", this.newPost)
        .then((response) => {
          console.log(response);
          this.$router.push("/posts");
        })
        .catch((error) => {
          this.errors = error.response.data.errors;
          console.log(this.errors);
        });
    },
  },
};
</script>

<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <form v-on:submit.prevent="createPost()">
      <p>
        Title:
        <input type="text" v-model="newPost.title" />
      </p>
      <p>
        Body:
        <input type="text" v-model="newPost.body" />
      </p>
      <small v-if="newPost?.body?.length > 0 && newPost?.body?.length <= 250">
        Remaining characters: {{ 250 - newPost?.body?.length }}
      </small>
      <small v-if="newPost?.body?.length > 250" class="text-danger">Post length can't exceed 250 characters.</small>
      <p>
        Image:
        <input type="text" v-model="newPost.image" />
      </p>
      <input type="submit" value="Create Post" />
    </form>
  </div>
</template>
