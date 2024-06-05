<script setup>
  import JSFileManager, { JSFile } from 'js-file-manager'
  import * as mmdb from 'music-metadata-browser';
  import { ref } from 'vue';
  import { FastAverageColor } from 'fast-average-color';
  import '../style/filepicker.css'

  const emits = defineEmits();
  const album_cover = ref('../src/assets/no_cover.png');
  const album_color = ref(null);

  const selectAudio = async () => {

    const fac = new FastAverageColor();

    // Pick and extract file data
    const audio_file = await JSFileManager.pick({ accept: ".mp3, .flac, .ogg, .wav" })
    const audio_url = await audio_file.getObjectURL();
    const audio_metadata = await mmdb.parseBlob(await audio_file.getBlob());

    // Setting Album Cover Image
    const image_buffer = mmdb.selectCover(audio_metadata.common.picture);
    if (image_buffer) {
      URL.revokeObjectURL(album_cover);
      album_cover.value = URL.createObjectURL(
        new Blob([image_buffer.data], { type: 'image/jpeg' })
      );
    } else album_cover.value = '../src/assets/no_cover.png';

    // Emit extracted values
    album_color.value = await fac.getColorAsync(album_cover.value, {
      algorithm: 'sqrt',
    });

    emits('file_select', audio_url, audio_metadata, album_color.value.hex);
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