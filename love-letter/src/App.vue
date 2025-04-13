<script setup lang="ts">
import LoveLetter from './components/LoveLetter.vue'
import PixelBackground from './components/PixelBackground.vue'
</script>

<template>
  <PixelBackground />
  <LoveLetter />
</template>

<style>
html, body {
  margin: 0;
  padding: 0;
  height: 100%;
  width: 100%;
  overflow: hidden;
}

#app {
  width: 100%;
  height: 100vh;
  margin: 0;
  padding: 0;
}
</style>
