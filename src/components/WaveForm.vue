<script setup>
  import WaveSurfer from 'wavesurfer.js';
  import { onBeforeUnmount, onMounted, ref, watch } from 'vue';

  const props = defineProps({
    audio: String,
    is_playing: Boolean,
    album_color: String,
  })

  const emit = defineEmits();
  const waveform = ref(null);
  let wavesurfer = null;

  onMounted(() => {
    wavesurfer = WaveSurfer.create({
      container: waveform.value,
      normalize: false,
      waveColor: '#444444',
      barWidth: 5,
      barGap: 5,
      barRadius: 2,
      height: 100,
      barAlign: 'bottom',
      dragToSeek: true,
    });
  });

  watch(() => props.is_playing, () => {
    wavesurfer.playPause();
  })

  watch(() => props.audio, () => {
    wavesurfer.empty();
    wavesurfer.load(props.audio);
    if (props.album_color != "#000000") {
      wavesurfer.setOptions({ progressColor: props.album_color });
    } else {
      wavesurfer.setOptions({ progressColor: '#888888' });
    }
    // emit paused status for playbackbtn
    emit("setPlayBackStatus", wavesurfer.isPlaying());
  })

  onBeforeUnmount(() => wavesurfer.destroy());
</script>

<template>
  <div class="waveform" ref="waveform"></div>
</template>