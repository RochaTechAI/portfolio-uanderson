<template>
  <div v-if="isLoading" class="loader-container">
    
    <!-- Word "PORTFOLIO" -->
    <div class="letters-container">
      <span v-for="(char, i) in text" :key="i" :class="['char', 'char-' + i]">
        {{ char }}
      </span>
    </div>

    <!-- Nome e Cargo (Aparecem logo após) -->
    <div class="sub-intro">
      <h2 class="name-text">UANDERSON ROCHA</h2>
      <p class="role-text">ESPECIALISTA EM ENGENHARIA DE SOFTWARE</p>
    </div>

    <div class="progress-bar-container">
      <div class="progress-fill" :style="{ width: `${progress}%` }"></div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import gsap from 'gsap'

const isLoading = ref(true)
const progress = ref(0)
const text = 'PORTFOLIO'.split('')

onMounted(() => {
  const tl = gsap.timeline({ 
    onComplete: () => gsap.to('.loader-container', { autoAlpha: 0, duration: 1.2, ease: "power2.inOut", onComplete: () => isLoading.value = false }) 
  });

  gsap.set('.char', { opacity: 0, y: 100, rotateX: -90, filter: 'blur(10px)' });
  gsap.set('.sub-intro', { opacity: 0, y: 20 });

  text.forEach((_, i) => {
    tl.to(`.char-${i}`, {
      opacity: 1, y: 0, rotateX: 0, filter: 'blur(0px)', duration: 0.4, ease: "back.out(2)"
    }, i * 0.08)
    .to(`.char-${i}`, { color: '#2563EB', duration: 0.1, yoyo: true, repeat: 1 }, i * 0.08);
    progress.value = (i + 1) * 11.1;
  });

  // Aparece o Nome e Cargo no final
  tl.to('.sub-intro', { opacity: 1, y: 0, duration: 0.8, ease: "power2.out" }, "+=0.2");
})
</script>

<style scoped>
.loader-container { 
  @apply fixed inset-0 z-[9999] bg-[#111827] flex flex-col items-center justify-center gap-6; 
}
.letters-container { @apply flex text-5xl md:text-7xl font-black text-white tracking-[0.2em] uppercase; perspective: 1000px; }
.sub-intro { @apply text-center mt-4; }
.name-text { @apply text-white text-xl md:text-2xl font-light tracking-[0.4em] uppercase; }
.role-text { @apply text-[#2563EB] text-xs md:text-sm font-medium tracking-[0.2em] uppercase mt-2; }
.progress-bar-container { @apply absolute bottom-20 w-32 h-[2px] bg-white/10; }
.progress-fill { @apply h-full bg-brand-blue shadow-[0_0_10px_#2563EB]; transition: width 0.5s ease; }
</style>