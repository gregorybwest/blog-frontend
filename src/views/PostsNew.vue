<script>
import axios from "axios";

export default {
  data: function () {
    return {
      newPostParams: { body: "" },
      errors: [],
      sadStatus: "",
    };
  },
  methods: {
    submit: function () {
      axios
        .post("/posts", this.newPostParams)
        .then((response) => {
          console.log("New Post", response.data);
          this.$router.push("/posts");
        })
        .catch((error) => {
          this.sadStatus = error.response.status;
          this.errors = error.response.data.errors;
        });
    },
  },
};
</script>

<template>
  <div class="posts-new">
    <div class="container">
      <form v-on:submit.prevent="submit()">
        <h1>New Post</h1>
        <div class="mb-3">
          <label for="postTitle" class="form-label">Title</label>
          <input type="title" v-model="newPostParams.title" class="form-control" id="postTitle" />
        </div>
        <div class="mb-3">
          <label for="postBody" class="form-label">Body</label>
          <input type="body" v-model="newPostParams.body" class="form-control" id="postBody" />
          <small class="danger">{{ 100 - newPostParams.body.length }} characters remaining</small>
        </div>
        <div class="mb-3">
          <label for="postImageUrl" class="form-label">Image Url</label>
          <input type="url" v-model="newPostParams.image" class="form-control" id="postImageUrl" />
        </div>
        <button type="submit" class="btn btn-primary">Submit</button>
      </form>
    </div>

    <!-- <div class="container">
      <form v-on:submit.prevent="submit()">
        <h1>New Post</h1>
        <img v-if="sadStatus" v-bind:src="`https://http.cat/${sadStatus}`" alt="" />
        <ul>
          <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
        </ul>
        <div>
          <label>Title:</label>
          <input type="text" v-model="newPostParams.title" />
          <br />
          <br />
        </div>
        <div>
          <label>Body:</label>
          <input type="text" v-model="newPostParams.body" />
          <br />
          <small class="danger">{{ 100 - newPostParams.body.length }} characters remaining</small>
          <br />
        </div>
        <div>
          <label>Image:</label>
          <input type="text" v-model="newPostParams.image" />
          <br />
        </div>
        <br />
        <input type="submit" value="Submit" />
      </form>
    </div> -->
  </div>
</template>

<style scoped>
.danger {
  color: rgb(171, 45, 45);
}
</style>
