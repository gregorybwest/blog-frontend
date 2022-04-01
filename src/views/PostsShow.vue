<script>
import axios from "axios";

export default {
  data: function () {
    return {
      post: {},
    };
  },
  created: function () {
    axios.get(`/posts/${this.$route.params.id}`).then((response) => {
      console.log(response.data);
      this.post = response.data;
    });
  },
  methods: {
    destroyPost: function () {
      axios.delete(`/posts/${this.post.id}`).then((response) => {
        console.log("Successfully deleted", response.data);
        this.$router.push("/posts");
      });
    },
  },
};
</script>

<template>
  <div class="posts-show">
    <div class="container">
      <img v-bind:src="post.image" alt="" />
      <h1>{{ post.title }}</h1>
      <h3>{{ post.body }}</h3>
      <div v-if="post.owner">
        <router-link v-bind:to="`/posts/${post.id}/edit`">Edit</router-link>
        <button v-on:click="destroyPost()">Delete</button>
      </div>
    </div>
  </div>
</template>

<style></style>
