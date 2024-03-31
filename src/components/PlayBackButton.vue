<script setup>
  import { ref } from 'vue';

  const emit = defineEmits();
  const is_playing = ref(false);

  const playBackOnClick = () => {
    is_playing.value = !is_playing.value;
    emit('setPlayBackStatus', is_playing.value);
  };

</script>

<template>
  <div  
    class="playback-btn btn btn-success mb-3"
    @click="playBackOnClick" 
  />
</template>