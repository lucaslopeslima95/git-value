<template>
  <div id="app">
    <navbar-component/>
    <router-view/>
  </div>
</template>

<script>
import navbarComponent from "./components/navbarComponent.vue";
export default{
  
  components:{navbarComponent}
}
</script>
<style>
#app{
  background-color: black;
  height:100vh;
}

</style>
