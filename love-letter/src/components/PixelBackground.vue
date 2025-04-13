<script setup lang="ts">
import { ref, onMounted, onUnmounted } from 'vue';

// Animation frame reference
const animationRef = ref<number | null>(null);

// Canvas reference
const canvasRef = ref<HTMLCanvasElement | null>(null);

// Setup the pixel background
onMounted(() => {
  const canvas = canvasRef.value;
  if (!canvas) return;

  const ctx = canvas.getContext('2d');
  if (!ctx) return;

  // Set canvas to full screen size
  function resizeCanvas() {
    canvas.width = window.innerWidth;
    canvas.height = window.innerHeight;
  }

  // Initial size
  resizeCanvas();

  // Resize listener
  window.addEventListener('resize', resizeCanvas);

  // Pixel grid settings
  const pixelSize = 20;
  const columns = Math.ceil(canvas.width / pixelSize);
  const rows = Math.ceil(canvas.height / pixelSize);

  // Colors
  const colors = ['#ffcce6', '#ffe6f2', '#ffb6e6', '#fff8f8'];

  // Create a grid
  const grid: number[][] = [];
  for (let y = 0; y < rows; y++) {
    grid[y] = [];
    for (let x = 0; x < columns; x++) {
      grid[y][x] = Math.floor(Math.random() * colors.length);
    }
  }

  // Animation state
  let time = 0;

  // Animation function
  function animate() {
    time += 0.02;
    
    // Clear canvas
    ctx.fillStyle = '#ffcce6';
    ctx.fillRect(0, 0, canvas.width, canvas.height);
    
    // Draw grid
    for (let y = 0; y < rows; y++) {
      for (let x = 0; x < columns; x++) {
        // Add pattern variations
        const patternValue = noise(x * 0.1, y * 0.1, time) * 3;
        const colorIndex = Math.floor(patternValue) % colors.length;
        
        // Only draw some pixels for a sparse effect
        if (Math.random() > 0.7) {
          ctx.fillStyle = colors[colorIndex];
          ctx.fillRect(
            x * pixelSize, 
            y * pixelSize, 
            pixelSize, 
            pixelSize
          );
        }
      }
    }
    
    // Continue animation
    animationRef.value = requestAnimationFrame(animate);
  }

  // Simple noise function for pattern generation
  function noise(x: number, y: number, z: number): number {
    const X = Math.floor(x) & 255;
    const Y = Math.floor(y) & 255;
    const Z = Math.floor(z) & 255;
    
    x -= Math.floor(x);
    y -= Math.floor(y);
    z -= Math.floor(z);
    
    const u = fade(x);
    const v = fade(y);
    const w = fade(z);
    
    // Simple hash function
    const hash = (n: number) => {
      return (Math.sin(n) * 43758.5453) % 1;
    };
    
    const a = hash(X) + Y;
    const aa = hash(a) + Z;
    const ab = hash(a + 1) + Z;
    const b = hash(X + 1) + Y;
    const ba = hash(b) + Z;
    const bb = hash(b + 1) + Z;
    
    return lerp(w, lerp(v, lerp(u, hash(aa), hash(ba)),
                           lerp(u, hash(ab), hash(bb))),
                  lerp(v, lerp(u, hash(aa + 1), hash(ba + 1)),
                           lerp(u, hash(ab + 1), hash(bb + 1))));
  }
  
  function fade(t: number): number {
    return t * t * t * (t * (t * 6 - 15) + 10);
  }
  
  function lerp(t: number, a: number, b: number): number {
    return a + t * (b - a);
  }

  // Start animation
  animate();

  // Cleanup
  onUnmounted(() => {
    if (animationRef.value) {
      cancelAnimationFrame(animationRef.value);
    }
    window.removeEventListener('resize', resizeCanvas);
  });
});
</script>

<template>
  <canvas ref="canvasRef" class="pixel-background"></canvas>
</template>

<style scoped>
.pixel-background {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  z-index: -1;
  image-rendering: pixelated;
}
</style> 