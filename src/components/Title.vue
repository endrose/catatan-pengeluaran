<template>

  <h1>{{ title}}</h1>
</template>

<script>
export default {
  name:"Title",
 props:{
   title: String
 }
}
</script>

<style scoped>
h1{
  color: blueviolet;
}
  h1, img{
    justify-content: center;

    text-align: center;
  }
 
</style>