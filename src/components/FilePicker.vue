<script setup>
  import JSFileManager, { JSFile } from 'js-file-manager'
  import * as mmdb from 'music-metadata-browser';
  import { ref } from 'vue';

  const emits = defineEmits();
  const album_cover = ref('../src/assets/no_cover.png');

  const selectAudio = async () => {

    // Pick File and emit audio and metadata
    const audio_file = await JSFileManager.pick({ accept: ".mp3, .flac, .ogg, .wav" })
    const audio_url = await audio_file.getObjectURL();
    const audio_metadata = await mmdb.parseBlob(await audio_file.getBlob());

    emits('file_select', audio_url, audio_metadata);

    // Setting Album Cover Image
    const image_buffer = mmdb.selectCover(audio_metadata.common.picture);
    if (image_buffer) {
      album_cover.value = URL.createObjectURL(
        new Blob([image_buffer.data], { type: 'image/jpeg' })
      );
    } else album_cover.value = '../src/assets/no_cover.png';
  }

</script>
<template>
  <div 
    @click="selectAudio" 
    class="cover-wrapper"
    :style="{backgroundImage: `url(${album_cover})`}"
    >
    <div class="cover-label">Select File</div>
  </div>
</template>


<style>

  .cover-wrapper {
    margin-left: 1.5rem;
    border: solid #ddd 5px;
    display: inline-block;
    background-size: contain;
    width: 500px;
    height: 500px;
    transition: 0.3s;
    display: flex;
    align-items: center;
    justify-content: center;
    background-color: #ddd;
    background-blend-mode: multiply;
  }
  
  .cover-wrapper:hover {
    background-color: #555;
    background-blend-mode: multiply;
    cursor: pointer;
    transition: 0.3s;
  }

  @keyframes fadeIn {
    0%   { opacity: 0; }
    100% { opacity: 1; }
  }
  
  
  .cover-label {
    width: 100%;
    height: 100%;
    font-size: 3rem;
    visibility: hidden;
    display: flex;
    justify-content: center;
    align-items: center;
  }
  
  .cover-wrapper:hover .cover-label {
    visibility: visible;
    animation: fadeIn 0.3s;
  }

</style>