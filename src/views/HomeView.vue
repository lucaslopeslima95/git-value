<template>
  <div id="home">
    <home-componet/>
  </div>
</template>

<script lang="ts">
import { Options, Vue } from 'vue-class-component';
import HomeComponet from '@/components/HomeComponet.vue';

@Options({
  components: {
    HomeComponet,
  },
})
export default class HomeView extends Vue {}
</script>

<style>
#home{
  margin-top: 70px;
}
</style>