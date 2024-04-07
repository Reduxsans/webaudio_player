<script setup>
  import Metadata from './Metadata.vue';
  import PlayBackButton from './PlayBackButton.vue';
  import WaveForm from './WaveForm.vue';
  import { ref } from 'vue';

  const props = defineProps({
    audio: String,
    metadata: Object,
    album_color: String,
  });
  
  const is_playing = ref(false);

  // Update PlayBack Button UI
  const setPlayBackStatus = (flag) => {
    is_playing.value = flag; 
  }

</script>

<template>
  <div class="player">

    <PlayBackButton 
      :is_playing="is_playing" 
      @setPlayBackStatus="setPlayBackStatus" 
    />
    
    <Metadata :metadata="metadata"/>
    
    <WaveForm 
      :is_playing="is_playing" 
      :audio="props.audio"
      :album_color="props.album_color"
      @setPlayBackStatus="setPlayBackStatus"
    />

  </div>
</template>