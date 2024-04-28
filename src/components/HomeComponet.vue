<template>
  <div class="container">
    <div class="d-flex justify-content-center align-items-center">
      <p class="titulo">Descubra quanto vale seu</p>
    </div>
      <div class="d-flex justify-content-center align-items-center flex-column">
        <img src="/public/img/gitlogo.jpg" id="git-logo">
        <p id="informe-seu-user">Informe o seu usuario do github aqui.</p>
        <input type="text" minlength="3" v-model="username" class="w-50">
        <button type="submit" class="btn btn-secondary mt-3 w-25" @click="buscaQuantidadeCommits()">Avaliar</button>
      </div>
  </div>
</template>

<script>
import Swal from 'sweetalert2/dist/sweetalert2.js'

export default {
    name:"HomeComponent",
    data(){
      return {
        username:""
      }
    },
    methods:{
      buscaQuantidadeCommits(){
        
          try {

              if(!this.username){
                  Swal.fire({
                    icon: "error",
                    title: "Oops... nome de usuario não pode ser vazio!",
                  });
                return
              }

              if(this.username.length<3){
                Swal.fire({
                    icon: "error",
                    title: "Nome de usuario inválido",
                  });
                return
              }

             this.$router.push({ 
                path: `/resultado`,query:{
                username:this.username
             } });

          } catch (error) {
              console.error('Erro ao obter a contagem de commits:', error);
          }
      }
    }

}
</script>

<style>
.container{
  background-color: black;
}
#git-logo{
  max-width: 50vw;
  max-height: 50vh;
}
.titulo{
  color:white;
  font-weight: bold;
  font-size: 42pt;
}
#informe-seu-user{
  color: white;
}
</style>