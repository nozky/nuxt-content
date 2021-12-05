<template>
  <div>
    <h1>{{ msg }}</h1>
  </div>
</template>

<script>
export default {
  props: ['msg']
}
</script>

<style scoped>
  div{
    display: flex;
    justify-content: center;
    border-radius: 5px;
    background-image: linear-gradient(to right, gray, lightgray);
  }
</style>