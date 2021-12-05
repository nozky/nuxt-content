<template>
  <div>
    <MainHeader class="main-header" :msg="msg" />
    <form v-on:submit.prevent> 
      <label for="search">Search</label>
      <input type="text" id="search" v-model="searchStr">
      <button @click="filterBlog(searchStr)">Search</button>
    </form>
    <button @click="fetchBlog">Get blog</button>
    <div class="blog-container">
      <ul>
        <li v-for="blog in blogs" :key="blog.slug">
          <nuxt-link :to="`/blog/${blog.slug}`"><h3>{{ blog.title }}</h3></nuxt-link>
          <p>{{ blog.description }}</p>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  mounted: function(){
    this.fetchBlog()
  },
  components: {},

  data(){
    return{
      //key: value 
      msg: 'Hello nuxt.js',
      blogs: null,
      searchStr: null
    }
  },

  methods: {
    fetchBlog: async function(){
      const response = await axios({
        url: '/_content/blog',
        method: 'GET',
      })
      this.blogs = response.data
    },
    filterBlog: function(searchStr){
      let regEx = new RegExp(searchStr,'gi')
      this.blogs = this.blogs.filter( blog => String(blog.title).match(regEx))
    }
  }
}
</script>

<style scoped>
  div{
    display: flex;
    flex-direction: column;
  }

  .main-header{
    text-align: center;
  }

  form{
    padding: 1rem;
    margin: 1rem;
  }

  input, label{
    width: 15ch;
    padding: 0.5rem;
    margin: 1rem;
    border-radius: 1px;
    cursor: pointer;
  }

  button{
    width: 15ch;
    padding: 0.5rem;
    margin: 1rem;
    border-radius: 1px;
    cursor: pointer;
  }
</style>