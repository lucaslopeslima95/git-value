<template>
    <div class="d-flex justify-content-center align-items-center vh-100">
        <ul class="d-flex justify-content-center align-items-center flex-column">
            <li><img height="250" width="250" :src="linkFotoPerfil" alt=""></li>
            <li class="list-item"><div class="campo-avaliado">Quantidade Commits públicos:</div></li>
            <li class="list-result">{{ this.quantidadeCommits }}</li>
            <li class="list-item"><div class="campo-avaliado">Avaliação do perfil:</div></li>
            <li class="list-result">{{ this.avaliacao }}</li>
            <li class="list-item"><div class="campo-avaliado">Cotação do perfil:</div></li>
            <li class="list-result"> {{ (this.quantidadeCommits*27.39).toLocaleString('pt-BR', { style: 'currency', currency: 'BRL' }) }}</li>
            <li><router-link to="/"><button class="btn btn-danger mt-5">Voltar</button></router-link> </li>
        </ul>
    </div>
  </template>
  
  <script>
  import axios from 'axios';
  
  export default {
      name:"ResultadoComponent",
      data(){
           return{
               username:"",
               quantidadeCommits:0,
               avaliacao:"",
               linkFotoPerfil:"img/perfil.jpeg"
           } 
      },
      created(){
          const searchParams = new URLSearchParams(window.location.search);
          const valorParametro = searchParams.get('username');
          this.montaResultado(valorParametro);
          this.linkFotoPerfil = this.getAvatarUrl(valorParametro);
      },
    methods:{
        async montaResultado(username){

            const response = await axios.get(`https:api.github.com/users/${username}/repos`);
            const repositorios = await response.data;

            let commitCount = 0;
               for (const repositorio of repositorios) {
                   const commitsResponse = await axios.get(`https://api.github.com/repos/${username}/${repositorio.name}/commits`);
                   const commits = commitsResponse.data;
                   commitCount += commits.length;
               }
            

            this.quantidadeCommits = commitCount;
            this.avaliacaoPerfil(commitCount)

            
        },
        avaliacaoPerfil(quantidadeCommits){

            if(quantidadeCommits<10){

                this.avaliacao = "Você é um Dev Fofinho!"
            }else if(quantidadeCommits<100){

                this.avaliacao = "Caramba ta mandando bem, continue assim!"
            }else{

                this.avaliacao = "Você é uma maquina de Codar!"
            }
        },
        async getAvatarUrl(username){

            try {
                const response  = await axios.get(`https://api.github.com/users/${username}`);
                const userData  = await response.data;
                const avatarUrl = await userData.avatar_url;
                
                if(!avatarUrl){
                    return "https://avatars.githubusercontent.com/u/79112366?v=4";
                }
                return avatarUrl;
            } catch (error) {
                console.error('Erro ao obter a URL da foto de perfil:', error);
                return;
            }
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