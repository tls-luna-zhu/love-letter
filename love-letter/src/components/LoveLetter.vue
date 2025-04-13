<script setup lang="ts">
import { ref } from 'vue';
import PixelHeart from './PixelHeart.vue';

// Message animation
const isMessageVisible = ref(false);

// Show message with typewriter effect
setTimeout(() => {
  isMessageVisible.value = true;
}, 500);
</script>

<template>
  <div class="love-letter-container">
    <div class="pixel-border"></div>
    <div class="love-letter">
      <div class="love-message" :class="{ 'visible': isMessageVisible }">
        I love you so much georgie!!!!!
      </div>
      <PixelHeart :size="70" color="#ff4d88" />
    </div>
  </div>
</template>

<style scoped>
.love-letter-container {
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
  position: relative;
  overflow: hidden;
}

/* Pixel art border around the entire screen */
.pixel-border {
  position: absolute;
  top: 20px;
  left: 20px;
  right: 20px;
  bottom: 20px;
  border: 8px solid #ff6eb4;
  box-shadow: 
    0 0 0 4px #fff,
    0 0 0 8px #ffb6e6;
  pointer-events: none;
  z-index: 10;
  image-rendering: pixelated;
}

.love-letter {
  position: relative;
  display: flex;
  align-items: center;
  justify-content: center;
  background-color: #fff8f8;
  border-radius: 16px;
  padding: 2rem 3rem;
  box-shadow: 
    0 8px 16px rgba(0, 0, 0, 0.1),
    0 0 0 4px #ffb6e6, /* Inner border */
    0 0 0 8px #fff8f8;
  image-rendering: pixelated;
  gap: 20px;
}

.love-message {
  font-family: 'Courier New', monospace;
  font-size: 28px;
  font-weight: bold;
  color: #ff6eb4;
  text-shadow: 2px 2px 0 #ffb6e6;
  letter-spacing: 1px;
  /* Typewriter effect */
  overflow: hidden;
  white-space: nowrap;
  width: 0;
  opacity: 0;
  transition: width 2s steps(30), opacity 0.1s;
}

.love-message.visible {
  width: 100%;
  opacity: 1;
}

/* For pixel art effect on text */
@media (max-width: 600px) {
  .love-message {
    font-size: 20px;
  }
  
  .love-letter {
    flex-direction: column;
    padding: 1.5rem 2rem;
  }
}
</style> 