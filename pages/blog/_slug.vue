<template>
  <div>
   <h1>Blog post</h1>
   <hr>
   <nuxt-content :document="doc" />
   <nuxt-link to="/">Home</nuxt-link>
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


</style>
