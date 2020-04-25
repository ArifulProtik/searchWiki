<template>
  <div>

    <div class="container">
      <div class="mg-top"></div>
      <div class="row">
        <div class="col-md"></div>
        <div class="col-md-6">
          <center>
            <div class="text-muted text-left up-text">
              Search any keyword...
            </div>
          <input 
          v-model="query" 
          type="text" 
          placeholder="Search..." 
          class="searchbox"
          v-on:keyup.enter="getSearch"
          
          >
          <div class="mg-top"></div>
          <Loader v-if="loader"/>
          </center>
        </div>
    <div class="col-md"></div>
      </div>
    </div>


    <div class="card-holder" v-for="post in posts" :key="post.id">
      <div class="mg-top">
        <div class="row">
          <div class="col-md"></div>
          <div class="col-md-6">
            <div class="card" style="">
              <img
                src="https://picsum.photos/600/300.jpg"
                class="card-img-top"
                alt=""
              />
              <div class="card-body">
                <h5 class="card-title">{{ post.title }}</h5>
                <p class="card-text">
                  {{post.intro}}... <span> <router-link :to="{name: 'post', params: {id: post.id}}">Continue Reading</router-link> </span>
                </p>
              </div>
            </div>
          </div>
          <div class="col-md"></div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Loader from "../components/Loader"
import axios from 'axios';
export default {
  name: "Home",
  components:{
    Loader
  },
  data(){
    return{
      posts: [],
      query: "",
      api_base: "https://getwiki.herokuapp.com/api/v1/",
      loader:false
    }
  },
  methods: {
    getSearch: function(){
      this.posts = []
      this.loader = true
      axios.get(`${this.api_base}search?q=${this.query}`)
      .then((result) => {
        console.log(result)
        result.data.forEach(item => {
          console.log(item)
          this.posts.push(item)
          this.loader = false
        });
      })
      .catch((error) => {
        console.log(error)
      })
    }
  }

}
</script>

<style scoped>
.searchbox{
  width: 100%;
  height: 48px;
  font-size: 16px;
  padding: 16px;
  border: 1.2px #ced4da solid;
  color: #495057;
  outline: none;
  border-radius: 0px 12px 0px 12px;
  transition-duration: 0.8s;
}
.searchbox:focus{
  border-radius: 12px 0px 12px 0px;
}
.up-text {
  font-size: 14px;
  margin-bottom: 8px;
  padding: 3px;
}
</style>

