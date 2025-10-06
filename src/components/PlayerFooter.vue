<script lang="ts" setup>
import { ref, useTemplateRef } from "vue";
import GuitarPng from "../assets/blogs/guitar.png?url";
import Song from "../assets/sound/Summer Acoustic Upbeat.mp3?url";

const audioPlayer = useTemplateRef<HTMLAudioElement>("audio-player");
// const hideMenu = ref(false);

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
    class="fixed z-20 bottom-0 right-0 transition-opacity duration-500 rounded-t-2xl mx-auto font-literata left-0 max-w-[1000px] bg-dark-slate text-light-olive-green shadow-xl"
  >
    <div class="flex justify-between items-center py-3 max-w-[900px] mx-auto">
      <!-- Volver -->
      <button
        onclick="window.location.href='/blogs'"
        class="flex gap-2 border-[1px] border-light-olive-green hover:bg-[#466868] px-4 py-2 rounded items-center text-light-olive-green transition-colors"
      >
        <!-- -->
        <slot name="back-icon" />
        <span class="text-xs">Más posts</span>
      </button>

      <audio ref="audio-player" :src="Song" loop></audio>
      <!-- Canción -->
      <button
        @click="playSound"
        class="flex items-center gap-2 text-light-olive-green"
      >
        <div class="hover:text-olive-green transition-colors">
          <slot v-if="isPaused" name="play-icon" />
          <slot v-else name="stop-icon" />
        </div>

        <img :src="GuitarPng" class="w-10 h-10 object-cover rounded" alt="" />
        <div class="flex flex-col justify-start">
          <span class="!text-sm !text-start font-semibold"
            >¿Quieres música para acompañar la lectura?</span
          >
          <p class="!text-xs !text-start text-gray-400">
            Summer Acoustic Upbeat - Bed · CorporateSounds
          </p>
        </div>
      </button>

      <div class="flex gap-5">
        <!-- <button
          onclick="window.scrollTo({top: 0, behavior: 'smooth'})"
          class="flex flex-col items-center text-light-olive-green hover:text-olive-green transition-colors"
        >
          <slot name="content-icon" />
          <span class="text-xs">Contenido</span>
        </button> -->
        <button
          onclick="window.scrollTo({top: 0, behavior: 'smooth'})"
          class="flex flex-col items-center text-light-olive-green hover:text-olive-green transition-colors"
        >
          <slot name="up-icon" />
          <span class="text-xs">Ir al menú</span>
        </button>
      </div>
    </div>
  </div>
</template>
