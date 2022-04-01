<script>
import axios from "axios";
import dayjs from "dayjs";
var relativeTime = require("dayjs/plugin/relativeTime");
dayjs.extend(relativeTime);

export default {
  data: function () {
    return {
      posts: [],
      titleFilter: "",
    };
  },
  created: function () {
    console.log("time: ", "dayjs().from(dayjs('1990-01-01')");
    axios.get("/posts").then((response) => {
      console.log(response.data);
      this.posts = response.data;
    });
  },
  methods: {
    filteredPosts: function () {
      return this.posts.filter((post) => {
        return post.title.toLowerCase().includes(this.titleFilter);
      });
    },
    relativeDate: function (date) {
      return dayjs().to(dayjs(date));
    },
  },
};
</script>

<template>
  <div class="posts-index">
    <div class="container">
      <p>
        Search:
        <input type="text" v-model="titleFilter" />
      </p>
      <datalist>
        <option v-for="post in posts" v-bind:key="post.id">
          {{ post.title }}
        </option>
      </datalist>
      <div class="row row-cols-2 row-cols-md-3 g-4">
        <transition-group
          appear
          enter-active-class="animate__animated animate__fadeIn"
          leave-active-class="animate__animated animate__fadeOut"
        >
          <div class="col" v-for="post in filteredPosts()" v-bind:key="post.id">
            <div class="card">
              <img v-bind:src="post.image" alt="" />
              <div class="card-body">
                <h5 class="card-title">{{ post.title }}</h5>
                <p class="card-text">
                  {{ post.body }}
                </p>
                <p>Created {{ relativeDate(post.created_at) }}</p>
                <router-link v-bind:to="`/posts/${post.id}`">
                  <button>Details</button>
                </router-link>
              </div>
            </div>
          </div>
        </transition-group>
      </div>
    </div>
    <!-- <p>
      Search:
      <input type="text" v-model="titleFilter" />
    </p>
    <datalist>
      <option v-for="post in posts" v-bind:key="post.id">
        {{ post.title }}
      </option>
    </datalist>
    <transition-group
      appear
      enter-active-class="animate__animated animate__fadeIn"
      leave-active-class="animate__animated animate__fadeOut"
    >
      <div v-for="post in filteredPosts()" v-bind:key="post.id">
        <router-link v-bind:to="`/posts/${post.id}`">
          <img v-bind:src="post.image" alt="" />
        </router-link>
        <h1>{{ post.title }}</h1>
        <h3>{{ post.body }}</h3>
        <h3>Created {{ relativeDate(post.created_at) }}</h3>
      </div>
    </transition-group> -->
  </div>
</template>

<style></style>
