<template>
  <div id="app">
      <my-navbar/>
    <router-view/>
  </div>
</template>
<script>
import MyNavbar from './components/MyNavbar.vue';
export default {
  components: {MyNavbar}
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
body {
  background-color: rgb(235, 228, 221);
}
nav {
  padding: 30px;
}

nav a {
  font-weight: bold;
  color: #2c3e50;
}

nav a.router-link-exact-active {
  color: #42b983;
}
</style>
