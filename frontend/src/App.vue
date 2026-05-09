<template>
  <div class="relative">
    <LoadingScreen />
    
    <main class="app">
      <h1 class="text-3xl font-bold underline p-10">
        Portfólio de Uanderson
      </h1>
    </main>
  </div>
</template>

<script setup>
import LoadingScreen from './components/LoadingScreen.vue'
</script>

<style>
.app {
  @apply relative z-10;
}
</style>