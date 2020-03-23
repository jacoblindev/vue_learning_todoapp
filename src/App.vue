<template>
  <div id="app">
    <Header/>
    <router-view/>
  </div>
</template>

<script>
import Header from './components/layout/Header'
export default {
  name: "app",
  components: {
    Header
  }
}
</script>
<style>
#app {
  font-family: Helvetica, sans-serif;
  text-align: left;
  color: #555;
}

#nav a {
  font-weight: bold;
}

#nav a.router-link-exact-active {
  color: #42b983;
}
</style>
