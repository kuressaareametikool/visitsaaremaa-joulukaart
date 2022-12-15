<script setup lang="ts">
import {Ref, ref} from "vue";
import Kristina from "./assets/Kristina_peajakeha.json";
import Sigrid from "./assets/Sigrid_peajakeha.json";
import Kati from "./assets/Kati_peajakeha.json";
import Saun from "./assets/saun.json";

const saun: Ref<any> = ref(null);
const kristina: Ref<any> = ref(null);
const kati: Ref<any> = ref(null);
const sigrid: Ref<any> = ref(null);

const temp = ref(25);
const active = ref(true);
const track = ref({
  cold: {
    status: false,
    segments: [240, 390],
    transition: [150, 240]
  },
  normal: {
    status: false,
    segments: [480, 620],
    transition: [390, 480]
  },
  warm: {
    status: false,
    segments: [780, 870],
    transition: [620, 780]
  },
  hot: {
    status: false,
    segments: [950, 1110],
    transition: [870, 950]
  },
})

const beginAnimation = () => {
  if (temp.value < 45) {
    kristina.value.playSegments([0, 150], true);
    kati.value.playSegments([0, 150], true);
    sigrid.value.playSegments([0, 150], true);
    return;
  }
  if (temp.value < 60) {
    if (!track.value.cold.status){
      kristina.value.playSegments(track.value.cold.transition, true);
      kati.value.playSegments(track.value.cold.transition, true);
      sigrid.value.playSegments(track.value.cold.transition, true);
      track.value.cold.status = true
    }
    kristina.value.playSegments(track.value.cold.segments);
    kati.value.playSegments(track.value.cold.segments);
    sigrid.value.playSegments(track.value.cold.segments);
    return;
  }
  if (temp.value < 75) {
    if (!track.value.normal.status){
      kristina.value.playSegments(track.value.normal.transition, true);
      kati.value.playSegments(track.value.normal.transition, true);
      sigrid.value.playSegments(track.value.normal.transition, true);
      track.value.normal.status = true
    }
    kristina.value.playSegments(track.value.normal.segments);
    kati.value.playSegments(track.value.normal.segments);
    sigrid.value.playSegments(track.value.normal.segments);
    return;
  }
  if (temp.value < 90) {
    if (!track.value.warm.status){
      kristina.value.playSegments(track.value.warm.transition, true);
      kati.value.playSegments(track.value.warm.transition, true);
      sigrid.value.playSegments(track.value.warm.transition, true);
      track.value.warm.status = true
    }
    kristina.value.playSegments(track.value.warm.segments);
    kati.value.playSegments(track.value.warm.segments);
    sigrid.value.playSegments(track.value.warm.segments);
    return;
  }
  if (!track.value.hot.status){
    kristina.value.playSegments(track.value.hot.transition, true);
    kati.value.playSegments(track.value.hot.transition, true);
    sigrid.value.playSegments(track.value.hot.transition, true);
    track.value.hot.status = true
  }
  kristina.value.playSegments(track.value.hot.segments);
  kati.value.playSegments(track.value.hot.segments);
  sigrid.value.playSegments(track.value.hot.segments);
  return;
};

const fireWood = () => {
  if (active.value) {
    active.value = false
    saun.value.goToAndPlay(0);
  }
}

const addHeat = () => {
  active.value = true;
  if (temp.value < 100) {
    temp.value += Math.round(Math.random() * 20)
    return;
  }
}

</script>
<template>
  <div class="flex flex-col gap-2 items-center">
    <h2 class="text-indigo-500 font-bold italic">Saunas on {{ temp }}ºC</h2>
    <div class="relative">
      <Vue3Lottie
        ref="saun"
        :animationData="Saun"
        :height="800"
        :width="800"
        :autoPlay="false"
        :loop="false"
        @onComplete="addHeat"
      />
      <div class="absolute top-12 left-4">
        <Vue3Lottie
          ref="kristina"
          :animationData="Kristina"
          :height="400"
          :width="400"
          :autoPlay="false"
          :loop="false"
          @onAnimationLoaded="beginAnimation"
          @onComplete="beginAnimation"
        />
      </div>
      <div class="absolute top-16 left-40 z-10">
        <Vue3Lottie
            ref="kati"
            :animationData="Kati"
            :height="400"
            :width="400"
            :autoPlay="false"
            :loop="false"
            @onAnimationLoaded="beginAnimation"
            @onComplete="beginAnimation"
        />
      </div>
      <div class="absolute top-20 right-20">
        <Vue3Lottie
            ref="sigrid"
            :animationData="Sigrid"
            :height="400"
            :width="400"
            :autoPlay="false"
            :loop="false"
            @onAnimationLoaded="beginAnimation"
            @onComplete="beginAnimation"
        />
      </div>
      <div class="absolute h-32 w-48 bottom-4 left-[280px] hover:cursor-pointer" @click="fireWood"></div>
    </div>
  </div>
</template>
