<script setup>
import { PauseIcon, PlayIcon, StopIcon } from "@heroicons/vue/24/solid";
import { ref } from "vue";
import Lego from "./assets/lego.json";

const anim = ref(null);

const play = () => anim.value.play();
const stop = () => anim.value.stop();
const pause = () => anim.value.pause();
</script>
<template>
  <div class="flex flex-col gap-2 items-center">
    <Vue3Lottie ref="anim" :animationData="Lego" :height="400" :width="400" />
    <div class="flex gap-2">
      <button
        class="bg-green-400 px-4 py-2 rounded shadow-md active:scale-90 text-white"
        @click="play"
      >
        <PlayIcon class="h-4 w-4" />
      </button>
      <button
        class="bg-yellow-400 px-4 py-2 rounded shadow-md active:scale-90 text-white"
        @click="pause"
      >
        <PauseIcon class="h-4 w-4" />
      </button>
      <button
        class="bg-red-400 px-4 py-2 rounded shadow-md active:scale-90 text-white"
        @click="stop"
      >
        <StopIcon class="h-4 w-4" />
      </button>
    </div>
  </div>
</template>
