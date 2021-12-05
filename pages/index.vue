<template>
  <div>
    <MainHeader class="main-header" :msg="msg" />
    <form v-on:submit.prevent> 
      <label for="search">Search</label>
      <input type="text" id="search" v-model="searchStr" @keyup="filterBlog(searchStr)"/>
    </form>
    
    <div class="blog-container">
      <ul v-for="blog in filteredBlogs" :key="blog.slug">
        <li>
          <BlogItem :blog="blog" /> 
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
    this.filteredBlogs = this.blogs //initialize when mounted
  },

  data(){
      return{
        //key: value 
        msg: 'Welcome to my blog',
        blogs: null,
        searchStr: null,
        filteredBlogs: null
      }
  },

  methods: {
     filterBlog: function(searchStr){
      let regEx = new RegExp(searchStr,'gi')
      this.filteredBlogs =  this.blogs.filter( blog => String(blog.title).match(regEx))
    },
    textChangeHandler: function(e){
      console.log(e.target.value)
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
    padding: 0.5rem;
    margin: 1rem;
  }

  input, label{
    width: 15ch;
    padding: 0.5rem;
    border-radius: 5px;
    cursor: pointer;
    outline: none;
  }

  button{
    width: 10ch;
    padding: 0.5rem;
    margin: 1rem;
    border-radius: 5px;
    cursor: pointer;
  }

  li{
    list-style: none;
    padding: 1rem;
    border: 1px solid lightgray;
    border-radius: 5px;
  }


</style>