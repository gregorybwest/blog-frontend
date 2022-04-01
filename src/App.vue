<script>
export default {
  data: function () {
    return {
      isLoggedIn: !!localStorage.jwt,
      flashMessage: null,
    };
  },
  watch: {
    $route: function () {
      this.isLoggedIn = !!localStorage.jwt;
      this.flashMessage = localStorage.flashMessage;
      localStorage.removeItem("flashMessage");
    },
  },
  methods: {},
};
</script>

<template>
  <nav class="navbar navbar-expand-lg navbar-light bg-light">
    <div class="container-fluid">
      <a class="navbar-brand" href="#">Blogs</a>
      <button
        class="navbar-toggler"
        type="button"
        data-bs-toggle="collapse"
        data-bs-target="#navbarNavAltMarkup"
        aria-controls="navbarNavAltMarkup"
        aria-expanded="false"
        aria-label="Toggle navigation"
      >
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse" id="navbarNavAltMarkup">
        <div class="navbar-nav">
          <router-link class="nav-link active" v-if="!isLoggedIn" to="/signup">Signup</router-link>
          <router-link class="nav-link" v-if="!isLoggedIn" to="/login">Login</router-link>
          <router-link class="nav-link" v-if="isLoggedIn" to="/logout">Logout</router-link>
          <router-link class="nav-link" v-if="isLoggedIn" to="/posts/new">Create Post</router-link>
          <router-link class="nav-link" to="/posts">Posts</router-link>
        </div>
      </div>
    </div>
  </nav>
  <div v-if="flashMessage">
    {{ flashMessage }}
    <button v-on:click="flashMessage = ''">Dismiss</button>
  </div>
  <router-view />
</template>
