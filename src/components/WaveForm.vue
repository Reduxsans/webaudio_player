<script setup>
  import WaveSurfer from 'wavesurfer.js';
  import { onBeforeUnmount, onMounted, onUpdated, ref, watch } from 'vue';

  const props = defineProps({
    audio: String,
    is_playing: Boolean,
  })

  const waveform = ref(null);
  let wavesurfer = null;

  onMounted(() => {
    wavesurfer = WaveSurfer.create({
      container: waveform.value,
      normalize: false,
      waveColor: 'white',
      progressColor: 'skyblue',
      barWidth: 6,
      barGap: 3,
      barRadius: 2,
      height: 100,
      barAlign: 'bottom',
      dragToSeek: true,
    });
  });

  watch(() => props.is_playing, (newVal, oldVal) => {
    wavesurfer.playPause();
  })

  watch(() => props.audio, (newVal, oldVal) => {
    wavesurfer.empty();
    wavesurfer.load(props.audio);
  })

  onBeforeUnmount(() => wavesurfer.destroy());
</script>

<template>
  <div class="waveform" ref="waveform"></div>
</template>