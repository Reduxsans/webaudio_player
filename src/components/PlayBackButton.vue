<script setup>
  import { ref } from 'vue';

  const emit = defineEmits();
  const props = defineProps({
    is_playing: Boolean,
  })

  const playBackOnClick = () => {
    const is_playing = !props.is_playing;
    emit('setPlayBackStatus', is_playing);
  };

</script>

<template>
  <button  
    class="playback-btn btn btn-success mb-3"
    @click="playBackOnClick" >
  {{ props.is_playing ? "Playing": "Paused" }}
  </button>
</template>