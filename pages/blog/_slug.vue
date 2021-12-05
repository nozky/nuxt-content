<template>
  <div>
   <h1>Blog post</h1>
   <hr>
   <nuxt-content :document="doc" />
   <nuxtLink to="/"><p class="back">Back</p></nuxtLink>
  </div>

</template>

<script>
export default {
  async asyncData({ $content, params }){
    const doc = await $content('blog', params.slug).fetch()
    return { doc }
  }
}
</script>

<style scoped>
  div{
    display: flex;
    flex-direction: column;
    justify-content: center;
    background-color: gray;
    padding: 1rem;
    border-radius: 5px;
  }

  hr{
    width: 100%;
  }

  .back{
    border: 1px solid gray;
    padding: 0.2rem;
    color: blue;
  }

  a{
    text-decoration: none;
  }


</style>
