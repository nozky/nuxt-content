<template>
  <div>
    <MainHeader class="main-header" :msg="msg" />
    <form v-on:submit.prevent> 
      <label for="search">Search</label>
      <input type="text" id="search" v-model="searchStr">
      <button @click="filterBlog(searchStr)">Search</button>
    </form>
    
    <div class="blog-container">
      <ul v-for="blog in blogs" :key="blog.slug">
        <li>
          <h3>
            <nuxt-link :to="`/blog/${blog.slug}`">{{ blog.title }}</nuxt-link>
            <p>{{ blog.description }}</p>
          </h3>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {

  head(){
    return{
      script: [{ src: 'https://identity.netlify.com/v1/netlify-identity-widget.js' }],
    }
  },

  async asyncData({$content, params}){
    const docs = await $content('blog').fetch()
    console.log( docs )
    return { docs }
  },

  mounted() {
    this.blogs = this.docs
  },

  data(){
      return{
        //key: value 
        msg: 'Welcome to my blog',
        blogs: null,
        searchStr: null
      }
  },

  methods: {
     filterBlog: function(searchStr){
      let regEx = new RegExp(searchStr,'gi')
      this.blogs =  this.blogs.filter( blog => String(blog.title).match(regEx))
    }
  },
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