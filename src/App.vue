<template>
  <div id="app" class="position-relative">
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
  background-color: #040707;
  height:92.36vh;
}

</style>
