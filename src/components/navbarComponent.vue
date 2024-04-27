<template>
  <nav class="navbar navbar-expand-lg bg-body-tertiary fixed-top">
  <div class="container-fluid">
    <router-link class="navbar-brand" to="/"><img height="50" width="150" src="img/logo2.png" alt="Logo"></router-link>
    <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNavDropdown" aria-controls="navbarNavDropdown" aria-expanded="false" aria-label="Toggle navigation">
      <span class="navbar-toggler-icon"></span>
    </button>
    <div class="collapse navbar-collapse" id="navbarNavDropdown">
      <ul class="navbar-nav w-100 d-flex justify-content-end ">
        <li>
          <p id="title" class="fs-4 self-align-end">Desenvolvedor Web Full Stack</p>
        </li>
      </ul>
    </div>
  </div>
</nav>
</template>

<script>
export default {
    name:"navbarComponent"

}
</script>

<style>
#title{
  font-family: Arial, Helvetica, sans-serif;
  font-weight: bold;
}
</style>