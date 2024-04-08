<script setup>
  import FilePicker from './components/FilePicker.vue';
  import Player from './components/Player.vue';
  import { ref } from 'vue';
  import './style/app.css'

  const audio = ref(null);
  const metadata = ref(null);
  const album_color = ref('#EEEEEE');

  const fileSelected = (audio_url, audio_metadata, fac_color) => {
    audio.value = audio_url;
    metadata.value = audio_metadata.common;
    album_color.value = fac_color;
  }

</script>

<template>
  <div class="content container-fluid">

    <div class="d-flex w-100">
      <FilePicker 
        @file_select="fileSelected"
      />
      <Player 
        :audio="audio"
        :metadata="metadata"  
        :album_color="album_color"
      />
    </div>

  </div>
</template>