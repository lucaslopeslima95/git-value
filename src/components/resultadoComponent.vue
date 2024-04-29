<template>
    <modal-load-component v-show="modalLoading"/>
    <ul class="d-flex justify-content-center align-items-center flex-column">
        <li><img height="250" width="250" :src="linkFotoPerfil" alt=""></li>
        <li class="list-item"><div class="campo-avaliado">Quantidade Commits públicos:</div></li>
        <li class="list-result">{{ this.quantidadeCommits }}</li>
        <li class="list-item"><div class="campo-avaliado">Avaliação do perfil:</div></li>
        <li class="list-result">{{ this.avaliacao }}</li>
        <li class="list-item"><div class="campo-avaliado">Cotação do perfil:</div></li>
        <li class="list-result"> {{ (this.quantidadeCommits*37.45).toLocaleString('pt-BR', { style: 'currency', currency: 'BRL' }) }}</li>
        <li><router-link to="/"><button class="btn btn-danger mt-5">Voltar</button></router-link></li>
    </ul>
</template>
  
  <script>
  import Swal from 'sweetalert2/dist/sweetalert2.js';
  import ModalLoadComponent from './ModalLoadComponent.vue';

  export default {
  components: { ModalLoadComponent },
      name:"ResultadoComponent",
      data(){
           return{
               username:"",
               quantidadeCommits:0,
               avaliacao:"",
               linkFotoPerfil:"img/perfil.jpeg",
           } 
      },
      created(){

          this.modalLoading = true;
          const searchParams = new URLSearchParams(window.location.search);
          const valorParametro = searchParams.get('username');
          
          this.montaResultado(valorParametro);
          this.getAvatarUrl(valorParametro);
      },
    methods:{
        async montaResultado(username){

            const response = await fetch(`https://api.github.com/users/${username}/repos`);
            const repositorios = await response.json(); 

            if(!this.isIterable(repositorios)){
                  Swal.fire({
                    icon: "warning",
                    title: "Oops...Não encontrei seu perfil",
                  });
                return
            }

            let commitCount = 0;
            for (const repositorio of repositorios) {
                const commitsResponse = await fetch(`https://api.github.com/repos/${username}/${repositorio.name}/commits`);
                const commits = await commitsResponse.json();
                commitCount += commits.length;
            }
            this.quantidadeCommits = commitCount;
            this.avaliacaoPerfil(commitCount);
            
        },
        avaliacaoPerfil(quantidadeCommits){

            if(quantidadeCommits<10){

                this.avaliacao = "Você é um Dev Fofinho!"
            }else if(quantidadeCommits<100){

                this.avaliacao = "Caramba ta mandando bem, continue assim!"
            }else{

                this.avaliacao = "Você é uma maquina de Codar!"
            }
            this.modalLoading = false;
        },
        async getAvatarUrl(username){

            try {

                const response = await fetch(`https://api.github.com/users/${username}`);
                const userData = await response.json(); 

                if(userData.avatar_url){

                    this.linkFotoPerfil = userData.avatar_url;
                    return    
                }
                this.linkFotoPerfil = "img/perfil.jpeg";
            } catch (error) {
                console.error('Erro ao obter a URL da foto de perfil:', error);
                return;
            }
        },
        isIterable(obj) {
            return typeof obj === 'object' && typeof obj[Symbol.iterator] === 'function';
        }
    }
  }
  </script>
  
  <style scoped>

  ul{
    list-style: none;
    color: aliceblue;
  }
  img{
    border-radius: 50%;
  }
  .list-item{
    
    font-size: 25pt;
    margin-bottom: 6px;
  }

  .campo-avaliado{
    font-weight: bold;
  }

  .list-result{
    margin-bottom: 30px;
    font-size: 20pt;
  }

  
  </style>