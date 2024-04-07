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
    class="playback-btn mb-3"
    @click="playBackOnClick"
    :class="[props.is_playing ? 'btn-pause' : 'btn-play']"
  />
</template>

<style>
  .btn-pause {
    background-image: url('../assets/pause.svg');
  }

  .btn-play {
    background-image: url('../assets/play.svg');
  }

  .playback-btn {
    width: 60px;
    height: 60px;
    border-radius: 30px;
    background-size: contain;
    border: none;
    background-color: transparent;
  }
</style>