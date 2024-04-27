<template>
    <div id="resultado">
        <resultado-component/>
    </div>
</template>

<script>
import resultadoComponent from '@/components/resultadoComponent.vue'


export default {
  components: { resultadoComponent },
  name:"ResultadoView",
   
}
</script>

<style>
#resultado{
    color: aliceblue;
    margin-top:70px;
}
</style>