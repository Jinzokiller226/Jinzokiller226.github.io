<script setup lang="ts">
import { RouterLink, RouterView } from 'vue-router'
import HelloWorld from './components/HelloWorld.vue'
</script>

<template>


      <div class=" bg-[url('../assets/bg.jpg')] w-max-screen-full bg-fixed  bg-center bg-no-repeat h-screen w-screen bg-cover  bg-gray-900/50 scrollable overflow-y-auto overflow-x-hidden">
        <RouterView />

      </div>



  
  
</template>

