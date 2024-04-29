<template>
    <div id="backdrop" class="position-absolute">
        <div id="modal-loading"  class="modal top-50 start-50 translate-middle"  data-backdrop="static">
            <div class="modal-dialog modal-sm">
                <div class="modal-content">
                    <div class="modal-body text-center">
                        <div class="loading-spinner mb-2 m-auto"></div>
                        <div>Carregando...</div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name:"ModalLoadComponent",
}
</script>

<style>

  #backdrop{
    background-color: rgb(64, 65, 61);
    height: 100%;
    width: 100%;
  }
  #modal-loading{
      display: block;
      color: black;
      max-height: 170px;
      
  }

  .loading-spinner{
        width:30px;
        height:30px;
        border:2px solid indigo;
        border-radius:50%;
        border-top-color:#0001;
        display: block;
        animation:loadingspinner .7s linear infinite;
    }

    @keyframes loadingspinner{
        0%{
            transform:rotate(0deg)
        }
        100%{
            transform:rotate(360deg)
        }
    }
</style>