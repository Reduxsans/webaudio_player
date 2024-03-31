<script setup>
  import FilePicker from './components/FilePicker.vue';
  import Player from './components/Player.vue';
  import { ref } from 'vue';

  const audio = ref(null);
  const metadata = ref(null);

  const fileSelected = (audio_url, audio_metadata) => {
    audio.value = audio_url;
    metadata.value = audio_metadata.common;
  }

</script>

<template>
  <div class="content container-fluid">

    <div class="d-flex w-100">
      <FilePicker @file_select="fileSelected"/>
      <Player 
        :audio="audio"
        :metadata="metadata"  
      />
    </div>

  </div>
</template>

<style>
  .content {
    margin-top: 10vh;
    display: flex;
    height: 100vh;
    justify-content: center;
    align-items: flex-start;
  }

  .playback-btn{
    width: 60px;
    height: 60px;
    border-radius: 30px !important;
  }

  .player {
    display: flex;
    justify-content: flex-start;
    flex-direction: column;
    width: 60vw;
    padding-left: 2rem;
  }
</style>

