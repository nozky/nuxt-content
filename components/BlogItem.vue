<template>
  <div class="blog-item">
   <div class="left">
     <div class="image-wrapper">
       <img :src="blog.thumbnail" :alt="blog.slug">
     </div>
   </div>
   <div class="right">
      <h3>{{ blog.title }}</h3>
    <nuxtLink :to="blog.path">
      <p>
      <span>{{ blog.date }}</span> <br>
      <span>{{ blog.author }}</span> <br>
      <span>{{ blog.description }}</span> <br>
      <div class="stars-container">
        <p>Rating: </p>
        <ul class="stars">
          <li v-for="star in blog.rating" :key="star">⭐️</li> 
        </ul>
      </div>
    </p>
    </nuxtLink>
   </div>
  </div>
</template>
<script>
export default {
  props:['blog']
}
</script>
<style scoped>
  .blog-item{
    display: flex;
    flex-direction: row;
  }

  .left{
    width: 150px;
    height: 150px;
    margin-right: 1rem;
    padding: 2rem;
  }


  .left .image-wrapper{
    border-radius: 50%;
    overflow: hidden;
  }

  .right{
    width: 80%;
  }

  img{
    width: 100%;
  }

  .stars-container{
    display: flex;
    align-items: center;
  }

  .stars-container .stars{
    display: flex;
    flex-direction: row;
    list-style: none;
    gap: 0.3rem;
  }
</style>