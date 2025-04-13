<script setup lang="ts">
import { ref, computed } from 'vue';

// Animation state
const isAnimating = ref(false);
const scale = ref(1);
const rotation = ref(0);
const sparkleOpacity = ref(0);

// Props for customization
const props = defineProps({
  size: {
    type: Number,
    default: 60
  },
  color: {
    type: String,
    default: '#ff4d88' // Pink heart color
  }
});

// Computed size for responsive scaling
const pixelSize = computed(() => props.size / 10);

// Animation function
function animate() {
  if (isAnimating.value) return;
  
  isAnimating.value = true;
  scale.value = 1;
  rotation.value = 0;
  sparkleOpacity.value = 0;
  
  // Animation sequence
  setTimeout(() => { scale.value = 1.3; }, 0);
  setTimeout(() => { rotation.value = 15; }, 100);
  setTimeout(() => { rotation.value = -15; sparkleOpacity.value = 1; }, 200);
  setTimeout(() => { rotation.value = 10; }, 300);
  setTimeout(() => { rotation.value = -5; }, 400);
  setTimeout(() => { rotation.value = 0; }, 500);
  setTimeout(() => { sparkleOpacity.value = 0; }, 600);
  setTimeout(() => { scale.value = 1; isAnimating.value = false; }, 700);
}
</script>

<template>
  <div 
    class="pixel-heart-container"
    @click="animate"
    :style="{ 
      transform: `scale(${scale}) rotate(${rotation}deg)`,
      width: `${props.size}px`,
      height: `${props.size}px`
    }"
  >
    <!-- Pixel Heart -->
    <div class="pixel-heart">
      <!-- Top row -->
      <div class="pixel" :style="{ 
        width: `${pixelSize}px`, 
        height: `${pixelSize}px`,
        top: `${pixelSize * 0}px`, 
        left: `${pixelSize * 2}px`,
        backgroundColor: props.color
      }"></div>
      <div class="pixel" :style="{ 
        width: `${pixelSize}px`, 
        height: `${pixelSize}px`,
        top: `${pixelSize * 0}px`, 
        left: `${pixelSize * 3}px`,
        backgroundColor: props.color
      }"></div>

      <div class="pixel" :style="{ 
        width: `${pixelSize}px`, 
        height: `${pixelSize}px`,
        top: `${pixelSize * 0}px`, 
        left: `${pixelSize * 6}px`,
        backgroundColor: props.color
      }"></div>
      <div class="pixel" :style="{ 
        width: `${pixelSize}px`, 
        height: `${pixelSize}px`,
        top: `${pixelSize * 0}px`, 
        left: `${pixelSize * 7}px`,
        backgroundColor: props.color
      }"></div>

      <!-- Second row -->
      <div class="pixel" :style="{ 
        width: `${pixelSize}px`, 
        height: `${pixelSize}px`,
        top: `${pixelSize * 1}px`, 
        left: `${pixelSize * 1}px`,
        backgroundColor: props.color
      }"></div>
      <div class="pixel" :style="{ 
        width: `${pixelSize}px`, 
        height: `${pixelSize}px`,
        top: `${pixelSize * 1}px`, 
        left: `${pixelSize * 2}px`,
        backgroundColor: props.color
      }"></div>
      <div class="pixel" :style="{ 
        width: `${pixelSize}px`, 
        height: `${pixelSize}px`,
        top: `${pixelSize * 1}px`, 
        left: `${pixelSize * 3}px`,
        backgroundColor: props.color
      }"></div>
      <div class="pixel" :style="{ 
        width: `${pixelSize}px`, 
        height: `${pixelSize}px`,
        top: `${pixelSize * 1}px`, 
        left: `${pixelSize * 4}px`,
        backgroundColor: props.color
      }"></div>
      <div class="pixel" :style="{ 
        width: `${pixelSize}px`, 
        height: `${pixelSize}px`,
        top: `${pixelSize * 1}px`, 
        left: `${pixelSize * 5}px`,
        backgroundColor: props.color
      }"></div>
      <div class="pixel" :style="{ 
        width: `${pixelSize}px`, 
        height: `${pixelSize}px`,
        top: `${pixelSize * 1}px`, 
        left: `${pixelSize * 6}px`,
        backgroundColor: props.color
      }"></div>
      <div class="pixel" :style="{ 
        width: `${pixelSize}px`, 
        height: `${pixelSize}px`,
        top: `${pixelSize * 1}px`, 
        left: `${pixelSize * 7}px`,
        backgroundColor: props.color
      }"></div>
      <div class="pixel" :style="{ 
        width: `${pixelSize}px`, 
        height: `${pixelSize}px`,
        top: `${pixelSize * 1}px`, 
        left: `${pixelSize * 8}px`,
        backgroundColor: props.color
      }"></div>

      <!-- Third through Seventh row (fill heart) -->
      <template v-for="row in 5" :key="`row-${row}`">
        <div 
          v-for="col in 10" 
          :key="`row-${row}-col-${col}`"
          class="pixel" 
          :style="{ 
            width: `${pixelSize}px`, 
            height: `${pixelSize}px`,
            top: `${pixelSize * (row+1)}px`, 
            left: `${pixelSize * (col-1)}px`,
            backgroundColor: props.color
          }"
        ></div>
      </template>

      <!-- Eighth row -->
      <template v-for="col in 8" :key="`row-8-col-${col}`">
        <div 
          class="pixel" 
          :style="{ 
            width: `${pixelSize}px`, 
            height: `${pixelSize}px`,
            top: `${pixelSize * 7}px`, 
            left: `${pixelSize * (col+0)}px`,
            backgroundColor: props.color
          }"
        ></div>
      </template>

      <!-- Ninth row -->
      <template v-for="col in 6" :key="`row-9-col-${col}`">
        <div 
          class="pixel" 
          :style="{ 
            width: `${pixelSize}px`, 
            height: `${pixelSize}px`,
            top: `${pixelSize * 8}px`, 
            left: `${pixelSize * (col+1)}px`,
            backgroundColor: props.color
          }"
        ></div>
      </template>

      <!-- Tenth row (point of heart) -->
      <template v-for="col in 4" :key="`row-10-col-${col}`">
        <div 
          class="pixel" 
          :style="{ 
            width: `${pixelSize}px`, 
            height: `${pixelSize}px`,
            top: `${pixelSize * 9}px`, 
            left: `${pixelSize * (col+2)}px`,
            backgroundColor: props.color
          }"
        ></div>
      </template>

      <!-- Last row (tip of heart) -->
      <template v-for="col in 2" :key="`row-11-col-${col}`">
        <div 
          class="pixel" 
          :style="{ 
            width: `${pixelSize}px`, 
            height: `${pixelSize}px`,
            top: `${pixelSize * 10}px`, 
            left: `${pixelSize * (col+3)}px`,
            backgroundColor: props.color
          }"
        ></div>
      </template>
    </div>

    <!-- Sparkles -->
    <div 
      class="sparkles"
      :style="{ opacity: sparkleOpacity }"
    >
      <div class="sparkle sparkle-1"></div>
      <div class="sparkle sparkle-2"></div>
      <div class="sparkle sparkle-3"></div>
      <div class="sparkle sparkle-4"></div>
    </div>
  </div>
</template>

<style scoped>
.pixel-heart-container {
  position: relative;
  cursor: pointer;
  transform-origin: center;
  transition: transform 0.1s ease-out;
  display: inline-block;
}

.pixel-heart {
  position: relative;
  width: 100%;
  height: 100%;
}

.pixel {
  position: absolute;
  background-color: #ff4d88;
}

.sparkles {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  pointer-events: none;
  opacity: 0;
  transition: opacity 0.3s ease-out;
}

.sparkle {
  position: absolute;
  background-color: #fff;
  width: 8%;
  height: 8%;
}

.sparkle-1 {
  top: -10%;
  left: 50%;
  clip-path: polygon(50% 0%, 61% 35%, 98% 35%, 68% 57%, 79% 91%, 50% 70%, 21% 91%, 32% 57%, 2% 35%, 39% 35%);
}

.sparkle-2 {
  top: 110%;
  left: 50%;
  clip-path: polygon(50% 0%, 61% 35%, 98% 35%, 68% 57%, 79% 91%, 50% 70%, 21% 91%, 32% 57%, 2% 35%, 39% 35%);
}

.sparkle-3 {
  top: 50%;
  left: -10%;
  clip-path: polygon(50% 0%, 61% 35%, 98% 35%, 68% 57%, 79% 91%, 50% 70%, 21% 91%, 32% 57%, 2% 35%, 39% 35%);
}

.sparkle-4 {
  top: 50%;
  left: 110%;
  clip-path: polygon(50% 0%, 61% 35%, 98% 35%, 68% 57%, 79% 91%, 50% 70%, 21% 91%, 32% 57%, 2% 35%, 39% 35%);
}
</style> 