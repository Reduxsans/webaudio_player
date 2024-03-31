<script setup>
  import Metadata from './Metadata.vue';
  import PlayBackButton from './PlayBackButton.vue';
  import WaveForm from './WaveForm.vue';
  import { ref } from 'vue';

  const props = defineProps({
    audio: String,
    metadata: Object
  })

  const is_playing = ref(false)
  const setPlayBackStatus = (flag) => {
    is_playing.value = flag;
  }

</script>

<template>
  <div class="player">
    <PlayBackButton @setPlayBackStatus="setPlayBackStatus" />
    <Metadata :metadata="metadata"/>
    <WaveForm :is_playing="is_playing" :audio="props.audio"/>
  </div>
</template>