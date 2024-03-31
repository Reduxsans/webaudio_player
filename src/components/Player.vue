<script setup>
  import Metadata from './Metadata.vue';
  import { ref } from 'vue';

  const props = defineProps({
    audio: Object,
    metadata: Object
  })

  const player = ref(null)

  const audioPlayback = () => {
    if (player.value) player.value.pause();
    
    player.value = new Audio(props.audio);
    player.value.load();
    player.value.play();
  }
</script>

<template>
  <div class="player">
    <div  
      class="playback-btn btn btn-success mb-3"
      @click="audioPlayback" 
    />
    <Metadata :metadata="metadata"/>
  </div>
</template>