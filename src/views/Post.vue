<template>
  <div>
      <div class="mg-top"></div>
    <center><Loader v-if="loader"/></center>
    <div v-for="post in posts" :key="post.id">
      <div class="card">
        <img src="https://picsum.photos/800/400.jpg" alt="" />
        <div class="card-body">
            <div class="mg-top"></div>
          <h1 class="card-title"> {{ post.title }}</h1>
          <div class="mg-top"></div>
          <p class="card-text">
            {{ post.body }}
          </p>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import axios from "axios";
import Loader from "../components/Loader";
export default {
  name: "post",
  components: {
    Loader,
  },
  data() {
    return {
      posts: [],
      loader: false,
    };
  },
  mounted() {
    this.getPostbyID();
  },
  methods: {
    getPostbyID: function() {
      var cid = this.$route.params.id;
      console.log(cid);
      this.loader = true;
      axios
        .get(`https://getwiki.herokuapp.com/api/v1/post/${cid}`)
        .then((result) => {
          this.posts.push(result.data);
          this.loader = false;
        })
        .catch((error) => {
          console.log(error);
        });
    },
  },
};
</script>
