<script>
import axios from "axios";

export default {
  data: function () {
    return {
      editPostParams: {},
      errors: [],
    };
  },
  created: function () {
    axios.get(`/posts/${this.$route.params.id}`).then((response) => {
      console.log(response.data);
      this.editPostParams = response.data;
    });
  },
  methods: {
    updatePost: function () {
      axios
        .patch(`/posts/${this.$route.params.id}`, this.editPostParams)
        .then((response) => {
          console.log("New Post", response.data);
          this.$router.push(`/posts/${response.data.id}`);
        })
        .catch((error) => {
          this.errors = error.response.data.errors;
        });
    },
  },
};
</script>

<template>
  <div class="posts-edit">
    <div class="container">
      <form v-on:submit.prevent="updatePost()">
        <h1>Edit Post</h1>
        <ul>
          <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
        </ul>
        <div>
          <label>Title:</label>
          <input type="text" v-model="editPostParams.title" />
        </div>
        <div>
          <label>Body:</label>
          <input type="text" v-model="editPostParams.body" />
        </div>
        <div>
          <label>Image:</label>
          <input type="text" v-model="editPostParams.image" />
        </div>
        <input type="submit" value="Update" />
      </form>
    </div>
  </div>
</template>
