<script lang="ts" setup>
import { ref, useTemplateRef } from "vue";

const audioPlayer = useTemplateRef<HTMLAudioElement>("audio-player");
// const hideMenu = ref(false);
defineProps({
  image: {
    type: String,
    required: true,
  },
  song: {
    type: String,
    required: true,
  },
  songTitle: {
    type: String,
    required: true,
  },
  author: {
    type: String,
    required: true,
  },
});

const isPaused = ref(true);
function playSound() {
  if (!audioPlayer.value) return;
  if (audioPlayer.value.paused) {
    audioPlayer.value.play();
    isPaused.value = false;
    return;
  }
  audioPlayer.value.pause();
  isPaused.value = true;
}
</script>

<template>
  <div
    class="fixed z-20 bottom-2 md:bottom-0 right-0 transition-opacity duration-500 rounded-t-2xl rounded-b-2xl md:rounded-b-none mx-2 md:mx-auto font-literata left-0 max-w-[1000px] bg-dark-slate text-light-olive-green shadow md:shadow-xl"
  >
    <div class="flex justify-between items-center px-4 md:px-0 py-3 max-w-[900px] mx-auto">
      <!-- Volver -->
      <button
        onclick="window.location.href='/blogs'"
        class="flex gap-2 md:border-[1px] border-light-olive-green hover:bg-[#466868] md:px-4 md:py-2 md:rounded items-center text-light-olive-green transition-colors"
      >
        <!-- -->
        <slot name="back-icon" />
        <span class="hidden md:block text-xs">Más posts</span>
      </button>

      <audio ref="audio-player" :src="song" loop></audio>
      <!-- Canción -->
      <button
        @click="playSound"
        class="flex items-center gap-2 px-5 text-light-olive-green"
      >
        <div class="hover:text-olive-green transition-colors">
          <slot v-if="isPaused" name="play-icon" />
          <slot v-else name="stop-icon" />
        </div>

        <img :src="image" class="w-10 h-10 hidden md:block object-cover rounded" alt="" />
        <div class="flex flex-col justify-start">
          <span class="text-xs md:text-sm text-start font-semibold"
            >¿Quieres música para acompañar la lectura?</span
          >
          <p class="!text-xs !text-start text-gray-400">
            {{ songTitle }} · {{ author }}
          </p>
        </div>
      </button>

      <div class="flex gap-5">
        <button
          onclick="window.scrollTo({top: 0, behavior: 'smooth'})"
          class="flex flex-col items-center text-light-olive-green hover:text-olive-green transition-colors"
        >
          <slot name="up-icon" />
          <span class="hidden md:block text-xs">Ir al menú</span>
        </button>
      </div>
    </div>
  </div>
</template>
