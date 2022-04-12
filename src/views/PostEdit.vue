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
  created: function () {
    axios.get(`/posts/${this.$route.params.id}`).then((response) => {
      this.newPost = response.data;
    });
  },
  methods: {
    editPost() {
      axios
        .patch(`/posts/${this.newPost.id}`, this.newPost)
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
    <h1>Edit Post</h1>
    <form v-on:submit.prevent="editPost()">
      <ul>
        <li v-for="error in errors" v-bind:key="error" style="color: red">
          {{ error }}
        </li>
      </ul>
      <p>
        Title:
        <input type="text" v-model="newPost.title" />
      </p>
      <p>
        Body:
        <input type="text" v-model="newPost.body" />
      </p>
      <p>
        Image:
        <input type="text" v-model="newPost.image" />
      </p>
      <input type="submit" value="Edit" />
    </form>
  </div>
</template>
