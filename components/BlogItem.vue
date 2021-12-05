<template>
  <div class="blog-item">
    <h3>{{ blog.title }}</h3>
    <nuxtLink :to="blog.path">
      <p>
      <span>{{ blog.date }}</span> <br>
      <span>{{ blog.author }}</span> <br>
      <span>{{ blog.description }}</span>
    </p>
    </nuxtLink>
  </div>
</template>
<script>
export default {
  props:['blog']
}
</script>
<style scoped>
  
</style>