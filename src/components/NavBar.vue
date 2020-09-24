<template>
  <div class="navbar">
    <h1>{{ title }}</h1>
  </div>
</template>

<script>
export default {
  name: 'NavBar',
  props: {
    title: String,
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.navbar {
  background: green;
  color: #fff;
  padding: 10px 0;
}
</style>
